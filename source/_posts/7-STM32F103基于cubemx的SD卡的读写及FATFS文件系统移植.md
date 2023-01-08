---
title: STM32F103基于cubemx的SD卡的读写及FATFS文件系统移植
date: 2021-08-02
updated: 2021-08-02
tags:
 - STM32
 - SD卡
 - FATFS文件系统
categories:
 - 嵌入式
 - STM32
keywords:
toc_number: false
top_img: https://img.pandior.ink/memory-cards-1426567_1920.jpg
cover: https://img.pandior.ink/sd-1138085_1920.jpg
copyright_author: 
copyright_author_href: 
copyright_url: 
copyright_info: 
katex: true
highlight_shrink: false
---

# STM32F103基于cubemx的SD卡的读写及FATFS文件系统移植

前言：之前一直对SD的读写感兴趣，这次刚好趁着和老师的项目有关系，就顺便学了一些皮毛，总的来说前前后后或多或少踩到了一些坑，在此记录。

# 一、SD卡相关内容

## 1、SD卡简介

在嵌入式项目中，经常会有要用到大容量存储的场景，SD卡提供了一种方便低廉的形式来储存数据。

> 提到储存，本来想介绍一下目前学习到的ROM、RAM、FLASH之间的区别的，但是与题无关，具体可以点击[这里](https://www.eefocus.com/embedded/466966)查看。总而言之，ROM掉电不丢失但是慢，RAM会丢失但是快，FLASH是后来技术水平上来集两家所长（读取速度快且不丢失），此外他们三个各有变种，不可一概而论。
>

本文SD卡主要采用STM32内部外设SDIO控制器完成与SD卡的数据传输。SDIO控制器不仅支持SD卡，还支持多媒体卡（ MMC 卡）、SD I/O 卡和 CE-ATA 设备等。（反正后面的这些乱七八糟的我活那么大都没见过，有个印象就行，反正正点原子的介绍讲了很多这些老套的，可能为了全面吧，我看的那是一个迷惑）

## 2、SDIO的引脚及其功能

SDIO引脚包括SDIO_CLK、SDIO_CMD、SDIO_D[3:0]。

|  引脚名称   |  功能  |                             说明                             |
| :---------: | :----: | :----------------------------------------------------------: |
|  SDIO_CLK   | 卡时钟 | 每个时钟周期在命令和数据线上传输1位命令或数据。时钟频率在0-25MHz |
|  SDIO_CMD   | 命令线 |                              无                              |
| SDIO_D[3:0] | 数据线 |                              无                              |

（另外现在能买到的SD卡基本上都是4位数据传输的，我就不做用一位数据传输的MMC卡等的介绍和代码分类了。）

此外 $SDIO\_CLK=\frac{HCLK}{2+CLKDIV}$​，这里的分频很重要，卡时钟不能超过SD卡所支持的最大操作频率，另外SD卡在刚初始化时时钟是不能超过400KHz否则容易失败，初始化完成以后就可以设置时钟频率到最大。

## 3、SDIO的通信协议

与正常的通信方式一样，SDIO也有一套完整的命令以及响应的协议，但是此协议过于底层，在此就不展开赘述，有兴趣的可自行上网了解，包括SDIO的寄存器操作。

下图为SDIO的读操作：

![https://img.pandior.ink/20210731220100.png](https://img.pandior.ink/20210731220100.png)

下图为SDIO的写操作：

![https://img.pandior.ink/20210731220223.png](https://img.pandior.ink/20210731220223.png)

此外补充一点，SDIO有一个FIFO寄存器，单片机对SD卡的读和写工作都是通过FIFO完成，FIFO相当于一个”粘合剂“！

## 4、SD卡的初始化流程

按照正点原子的初始化流程大约是以下这样：

![https://img.pandior.ink/20210731221121.png](https://img.pandior.ink/20210731221121.png)

他是对卡先进行分类、然后确定供电电压等等，标准库确实挺麻烦的，后面我们用到HAL库就没有这么多事情了，但是我个人认为了解一点底层和内部的关系终究没有坏处。

# 二、FATFA文件系统

## 1、FATFS系统简介

FATFS是一个免费开源的文件系统，如果想让SD卡里的东西在电脑上也能用（即兼容Windows系统），就必须要用上文件系统。FATFA系统最顶层是应用层，我们只需关注这一块，而系统内部的结构、复杂的协议我们无需理会。

![https://img.pandior.ink/20210731222453.png](https://img.pandior.ink/20210731222453.png)

其中，应用层是最后面我们使用的如f_open,f_write,f_close等。

中间层是FAT文件的读、写协议，非必要情况无需更改。

底层是我们需要修改移植的地方，主要是对存储媒介（本文是SD卡）的读、写接口对应以及创建、修改时种。（这个时钟我没用上）

## 2、系统移植

无需更改的文件：

|   文件名   |                 描述                 |
| :--------: | :----------------------------------: |
|    ff.h    |    FATFS 和应用模块公用的包含文件    |
|    ff.c    |              FATFS 模块              |
|  diskio.h  | FATFS 和 disk I/O 模块公用的包含文件 |
| interger.h |             数据类型定义             |
|   option   |   可选的外部功能（比如支持中文等）   |

需要更改的文件：

|  文件名  |                             描述                             |
| :------: | :----------------------------------------------------------: |
| ffconf.h | FATFS的配置文件，如支持读写还是只支持读、是否支持字符串操作、是否使能快速定位、语言类型设置等等 |
| diskio.c |                    单片机与SD卡通信的接口                    |

FATFS的移植主要分为以下几步：

- 数据类型： 在 integer.h 里面去定义好数据的类型。这里需要了解你用的编译器的数据类型，并根据编译器定义好数据类型。
- 配置： 通过 ffconf.h 配置 FATFS 的相关功能，以满足你的需要。
- 函数编写：打开 diskio.c ，进行底层驱动编写,一般需要编写 6 个接口函数，如下图所示：

![https://img.pandior.ink/20210731225016.png](https://img.pandior.ink/20210731225016.png)

# 三、cubemx配置

真的是特别感谢意法半导体公司出的这一款神器，可视化的配置大大缩短了STM32相关的项目开发时间。

上面我们讲的那一堆东西其实根本不需要懂（但是我也说过了，底层的东西了解一些没有坏处），只需要用鼠标点点点就可以轻松完成SD卡以及FATFS系统的移植。

1、选择使用的STM32芯片以及基本配置（时钟，串口调试等）

![https://img.pandior.ink/20210802220220.png](https://img.pandior.ink/20210802220220.png)

2、打开SDIO外设并设置

![https://img.pandior.ink/20210802211541.png](https://img.pandior.ink/20210802211541.png)

这里我们选择SD卡并且4位数据传输，前面也说过了，现在正常买到的卡都是支持4位的。

下面红框的选项非常的重要，我们之前也说过$SDIO\_CLK=\frac{HCLK}{2+CLKDIV}$，这里我们输入4，一般来说STM32F1单片机的主频工作在72MHz，这时SD卡的时钟就是12MHz，刚好可以满足要求，如果SD卡时钟速度过高可能会通讯失败。

3、打开全局中断

![https://img.pandior.ink/20210802211949.png](https://img.pandior.ink/20210802211949.png)

这里DMA开不开看个人选择，我本来是想打开的，但是F1好像DMA功能不全。

<font color=red>这里注意：如果配置DMA，在中断优先级配置里SDIO中断优先级必须大于DMA！</font>

4、移植FATFS系统

![https://img.pandior.ink/20210802212854.png](https://img.pandior.ink/20210802212854.png)

这里选择SD卡，下面具体设置里选择GBK编码（支持简体中文），同时选择支持长文件名并将动态工作区放在堆栈中。

cubemx上面的包括下面的一些设置，什么支持快速查找，最大长度之类的都是前面讲过的ffconf.h内的修改内容，这里可以直接在cubemx里选择，不能不说，cubemx，yyds！

5、SD卡插入检测

![https://img.pandior.ink/20210802213558.png](https://img.pandior.ink/20210802213558.png)

如果按部就班的按照上面的设置来，这里应该是选择不了的，这是一个检测SD卡是否插入的功能，如果在PCB板设计中标注了这个脚就按设计的来，如果没有就随便选择一个没有用到的引脚并设置为下拉（该引脚为低时SD卡插入）。

![https://img.pandior.ink/20210802213916.png](https://img.pandior.ink/20210802213916.png)

6、配置时钟树

![https://img.pandior.ink/20210802214045.png](https://img.pandior.ink/20210802214045.png)

> 时钟树配置真的是cubemx最厉害的地方之一，之前学标准库的时候，各种系统文件时钟配置真的又臭又长，如果有个地方有问题还很难发现，一般都是默认设置。现在直接图形化选择，我真的想知道那些用STM32十多年的老工程师会不会一口血吐在屏幕上 🤔
>
> 不过HAL库是官方主打的方向，标准库终究会退出这个时代！
>

言归正传，这里可以看到SDIO的时钟呵HCLK的时钟一致，在32其他高版本中可能可以单独设置SDIO的时钟，那另说。

7、设置堆栈大小

![https://img.pandior.ink/20210802215421.png](https://img.pandior.ink/20210802215421.png)

我们在第四步中将工作暂存区放在了堆栈中，所以默认的堆栈大小可能不能满足要求，这里需要扩充堆栈，0x400改成0x1000！

8、生成文件！

# 四、测试代码

可以看到cubemx帮我们把文件管理的特别有条理。

<img src="https://img.pandior.ink/20210802220929.png" alt="https://img.pandior.ink/20210802220929.png" style="zoom: 67%;" />

## 0、开始前的准备

在main函数开始前添加这一段代码完成printf的重定向。

```c
#ifdef __GNUC__
/* With GCC, small printf (option LD Linker->Libraries->Small printf
   set to 'Yes') calls __io_putchar() */
#define PUTCHAR_PROTOTYPE int __io_putchar(int ch)
#else
#define PUTCHAR_PROTOTYPE int fputc(int ch, FILE *f)
#endif /* __GNUC__ */

PUTCHAR_PROTOTYPE {
    /* Place your implementation of fputc here */
    /* e.g. write a character to the USART1 and Loop until the end of transmission */
    // 注意下面第一个参数是&huart1，因为cubemx配置了串口1自动生成
    HAL_UART_Transmit(&huart3, (uint8_t *) &ch, 1, 0xFFFF);
    return ch;
}

int _write(int file, char *ptr, int len) {
    int DataIdx;
    for (DataIdx = 0; DataIdx < len; DataIdx++) { __io_putchar(*ptr++); }
    return len;
}
```

## 1、定义变量

```
FATFS   fs;         /* FATFS 文件系统对象 */
FIL     fil;         /* FATFS 文件对象    */

uint32_t byteswritten;                /* File write counts */
uint32_t bytesread;                   /* File read counts */
uint8_t wtext[100] = "This is Pandior's blog!";                /* File write buffer */
uint8_t rtext[100];                   /* File read buffers */
char filename[50] = "sd_test";
```

其中fs为文件系统工作区；

fil为文件对象结构的指针；

`bytesread`/`byteswritten`分别存储读写的字节数；

`rtext`/`wtext`分别为读写缓存；

`filename`存储文件名（因为我们在前面使能了FATFS文件系统中的长文件名，最长255字节，若不支持长文件名，则文件名最多8个字节）。

## 2、输入测试代码

```c
   printf("\r\n ****** FatFs Example ******\r\n\r\n");
   retSD = f_mount(&fs, "", 0);
   if(retSD)
   {
       printf(" mount error : %d \r\n",retSD);
       Error_Handler();
   }
   else
       printf(" mount sucess!!! \r\n");
   /*##-2- Create and Open new text file objects with write access ######*/
   retSD = f_open(&fil, filename, FA_OPEN_ALWAYS|FA_WRITE);
   if(retSD)
       printf(" open file error : %d\r\n",retSD);
   else
       printf(" open file sucess!!! \r\n");

   /*##-3- Write data to the text files ###############################*/
//   f_lseek(&fil,fil.fptr+fil.fsize);//将指针指向文件末尾
   retSD = f_write(&fil, wtext, sizeof(wtext), (void *)&byteswritten);
   if(retSD)
       printf(" write file error : %d\r\n",retSD);

   retSD=f_write(&fil, "\r\n", sizeof("\r\n")-1, (void *)&byteswritten);
   if(retSD)
       printf(" write file error : %d\r\n",retSD);

   /*##-4- Close the open text files ################################*/
   retSD = f_close(&fil);
   if(retSD)
       printf(" close error : %d\r\n",retSD);
   else
       printf(" close sucess!!! \r\n");
```

这里完成的任务主要有：

- 注册一个文件系统对象
- 打开文件（如果没有则创建）
- 写文件
- 读文件

串口输出的结果如下：

![https://img.pandior.ink/20210803110602.png](https://img.pandior.ink/20210803110602.png)

如果有问题，串口会输出一个错误编码，在程序中是retSD（return SD：SD卡的返回值） 变量，这个变量的具体含义在ff.h文件中有详细描述，可根据返回错误类型进行针对性解决。

```c
FR_OK= 0,           /* (0) Succeeded */
FR_DISK_ERR,         /* (1) A hard error occurred in the low level disk I/O layer */
FR_INT_ERR,             /* (2) Assertion failed */
FR_NOT_READY,        /* (3) The physical drive cannot work */
FR_NO_FILE,             /* (4) Could not find the file */
FR_NO_PATH,             /* (5) Could not find the path */
FR_INVALID_NAME,      /* (6) The path name format is invalid */
FR_DENIED,          /* (7) Access denied due to prohibited access or directory full */
FR_EXIST,           /* (8) Access denied due to prohibited access */
FR_INVALID_OBJECT,    /* (9) The file/directory object is invalid */
FR_WRITE_PROTECTED,       /* (10) The physical drive is write protected */
FR_INVALID_DRIVE,     /* (11) The logical drive number is invalid */
FR_NOT_ENABLED,          /* (12) The volume has no work area */
FR_NO_FILESYSTEM,     /* (13) There is no valid FAT volume */
FR_MKFS_ABORTED,      /* (14) The f_mkfs() aborted due to any parameter error */
FR_TIMEOUT,             /* (15) Could not get a grant to access the volume within defined period */
FR_LOCKED,          /* (16) The operation is rejected according to the file sharing policy */
FR_NOT_ENOUGH_CORE,       /* (17) LFN working buffer could not be allocated */
FR_TOO_MANY_OPEN_FILES,    /* (18) Number of open files > _FS_SHARE */
FR_INVALID_PARAMETER/* (19) Given parameter is invalid */
```

**部分具体的错误类型及原因**

|      错误类型      |                           可能原因                           |
| :----------------: | :----------------------------------------------------------: |
|     FR_OK (0)      |                  函数成功，该文件对象有效。                  |
|     FR_NO_FILE     |                找不到该文件，可能没有创建成功                |
|     FR_NO_PATH     |                         找不到该路径                         |
|  FR_INVALID_NAME   |                          文件名无效                          |
|  FR_INVALID_DRIVE  |          驱动器号无效，主要是f_mount()这边的问题。           |
|      FR_EXIST      |                         该文件已存在                         |
|     FR_DENIED      | 由于下列原因，所需的访问被拒绝:1、以写模式打开一个只读文件；2、由于存在一个同名的只读文件或目录，而导致文件无法被创建；3、由于目录表或磁盘已满，而导致文件无法被创建。 |
|    FR_NOT_READY    | 由于驱动器中没有存储介质或任何其他原因，而导致磁盘驱动器无法工作 |
| FR_WRITE_PROTECTED |    在存储介质被写保护的情况下，以写模式打开或创建文件对象    |
|    FR_DISK_ERR     | 由于底层磁盘I/O接口函数中的一个错误，而导致该函数失败。     一般是移植或配置有问题 |
|     FR_INT_ERR     |    由于一个错误的FAT结构或一个内部错误，而导致该函数失败     |
|   FR_NOT_ENABLED   |                     逻辑驱动器没有工作区                     |
|  FR_NO_FILESYSTEM  |                    磁盘上没有有效地FAT卷                     |



## 3、相关函数介绍

### f_mount：在FatFs模块上注册、注销一个工作区

```c
FRESULT f_mount (
    FATFS* fs,         /* Pointer to the file system object (NULL:unmount)*/
    const TCHAR* path,    /* Logical drive number to be mounted/unmounted */
    BYTE opt           /* 0:Do not mount (delayed mount), 1:Mount immediately */
)
```

参数：

fs 工作区（文件系统对象）指针

path  注册/注销工作区的逻辑驱动器号

opt      注册或注销选项

> 在使用任何文件函数之前，必须使用f_mount函数为驱动器注册一个工作区。只有这样，其他文件函数才能正常工作。
>

### f_open：创建/打开一个用于访问文件的文件对象

```c
FRESULT f_open (
    FIL* fp,           /* Pointer to the blank file object */
    const TCHAR* path,    /* Pointer to the file name */
    BYTE mode          /* Access mode and file open mode flags */
)
```

参数：

fp   将被创建的文件对象结构的指针

path  文件名指针，指定将创建或打开的文件名

mode 访问类型和打开方法，由一下标准的一个组合指定的。

|      模式      |                             描述                             |
| :------------: | :----------------------------------------------------------: |
|    FA_READ     | 指定读访问对象。可以从文件中读取数据。 与FA_WRITE 结 合可以进行读写访问 |
|    FA_WRITE    | 指定写访问对象。可以向文件中写入数据。与FA_READ 结合 可以进行读写访问 |
| FA_OPEN_ALWAYS |     如果文件存在，则打开；否则，创建一个新文件（最好用）     |
| FA_CREATE_NEW  |          创建一个新文件。如果文件已存在，则创建失败          |

其实在我学习的过程中，绝大多数读写问题都是因为文件打开操作有问题。

比如说：

1、之前一直写不了第二次，就是写第二次的时候会把第一次覆盖掉，是因为我用了`FA_CREATE_ALWAYS`，每次复位都会创建一个新的文件替代。

2、写一直报错，错误代码是7，`FR_DENIED` ，原因是我在打开文件时没有|（或）上`FA_WRITE`，所以没有权限。

等等。

### f_close：关闭一个打开的文件

```c
FRESULT f_close (
    FIL *fp        /* Pointer to the file object to be closed */
)
```

参数：

fp 指向将被关闭的已打开的文件对象结构的指针

> 如果不关闭修改后的文件，那么文件可能会崩溃。
>

### f_read：从一个打开的文件中读取数据

```c
FRESULT f_read (
    FIL* fp,      /* Pointer to the file object */
    void* buff,        /* Pointer to data buffer */
    UINT btr,      /* Number of bytes to read */
    UINT* br       /* Pointer to number of bytes read */
)
```

参数：

fp  指向将被读取的已打开的文件对象结构的指针

buff  指向存储读取数据的缓冲区的指针

btr  要读取的字节数

br 指向返回已读取字节数的UINT变量的指针，返回为实际读取的字节数

### f_write：写入数据到一个已打开的文件

```
FRESULT f_write (
    FIL* fp,           /* Pointer to the file object */
    const void *buff, /* Pointer to the data to be written */
    UINT btw,          /* Number of bytes to write */
    UINT* bw           /* Pointer to number of bytes written */
)
```

参数：

fp  指向将被写入的已打开的文件对象结构的指针

buff  指向存储写入数据的缓冲区的指针

btr  要写入的字节数

br 指向返回已写入字节数的UINT变量的指针，返回为实际写入的字节数。

> FATFS还有很多其他的函数，具体可以到FASTFS的官网查阅。

