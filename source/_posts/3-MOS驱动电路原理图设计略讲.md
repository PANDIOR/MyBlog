---
title: MOS驱动电路原理图设计略讲
date: 2020-06-09 14:56:27
updated: 2020-08-04
tags:
- 电机驱动
- H桥电路
- MOSFET
categories:
- 竞赛
- 智能车
keywords:
description: 
- 实验室往年电机驱动一直用的BTN7971，设计的实在是不尽人意，而且这个内部集成十分完善的驱动完全学习不到任何东西，一天晚上，实验室另一位同学王鸿儒无意中发现的一个超低内阻（0.3mΩ）的mos管，引发了这次对于电机驱动的改进。
top_img: https://img.pandior.ink/motor-1461438_1920.jpg
comments: 
cover: https://img.pandior.ink/motor-1461438_1920.jpg
katex: true
---

# MOS驱动电路原理图设计略讲

**特别提示：本篇仅针对智能车制作而编写的MOS驱动电路设计，在此范围内不需考虑但其他场合很有必要的选型因素在此不作过多赘述，有兴趣自行学习。**



## TVS二极管

![TVS实物图](http://img.pandior.ink/image-20200726113714265.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

* 作用：瞬态抑制二极管是一种高效的电路保护器件，可以允许通过**上百安**的大电流来钳位电压。*类似于稳压二极管但是效果更好（稳压二极管电流在几十到几百mA，而TVS可以达到几到几十A）*。 当电路来了一个很大的电压脉冲（人体静电电压可达几百甚至上千伏），TVS可以在皮秒级别的时间里降低阻抗（雪崩击穿），反向击穿吸收电流，将电压钳位在设定的安全范围。

* 重要参数：

  * V<sub>BR</sub>（最小击穿电压）：TVS两端的电压称为最小击穿电压，类似于稳压二极管的稳压值。

  * V<sub>rwm</sub>（额定反向关断电压）:V<sub>rwm</sub>是TVS 最大连续工作的直流或脉冲电压，大于此电压电路会损坏，应该大于电路的正常工作电压。

  * V<sub>c</sub>（钳位电压）:出现浪涌现象时电路的最大电压，反映了TVS的浪涌抑制能力。V<sub>c</sub>必须小于电路的安全电压，V<sub>c</sub>一般大于V<sub>BR</sub>。

    >**保护过程**：
    >
    >在瞬态峰值脉冲电流作用下，流过TVS 的电流，由原来的反向漏电流I<sub>D</sub> 上升到I<sub>R</sub> 时，其两极呈现的电压由额定反向关断电压V<sub>rwm</sub>上升到击穿电压V<sub>BR</sub>，TVS 被击穿。随着峰值脉冲电流的出现，流过TVS 的电流达到峰值脉冲电流I<sub>pp</sub>。在其两极的电压被箝位到预定的最大箝位电压以下。然后，随着脉冲电流按指数衰减，TVS 两极的电压也不断下降，最后恢复到起始状态。这就是TVS 抑制可能出现的浪涌脉冲功率，保护电子元器件的整个过程。
    > **双向TVS（Bi）：**用于交流电或来自正负双向脉冲的场合。TVS有时也用于减少电容。如果电路只有正向电平信号，那么单向TVS就足够了。
    > **单向TVS（Uni）：**正向浪涌时,TVS处于反向雪崩击穿状态；反向浪涌时，TVS类似正向偏置二极管一样导通并吸收浪涌能量。

  （注：还有一些重要参数例如最大脉冲峰值电流I<sub>pp</sub>等没有说明，因为一般来说都能满足智能车需求）

~~不过智能车无脑选`SMAJ16CA` 就行了。~~

<img src="http://img.pandior.ink/image-20200531110624271.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/I0VDQUQ5RQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim" alt="TVS伏安特性曲线" style="zoom:67%;" />

## MOS 管选型

![IPT004N03L](http://img.pandior.ink/R1300929-01.jpg?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzQyNkZFQQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

1. 尽量选择R<sub>DS<sub>（on）</sub></sub>小的MOS，当MOS导通时损耗更小，发热少。

   * IPT004N03L的 R<sub>DS<sub>（on）</sub></sub>为0.3mΩ，我查阅了很多其他MOS的导通内阻，都没有发现比这个更小的。R<sub>DS<sub>（on）</sub></sub>小意味着电机驱动时发热量会更少，在MOS上的损耗也会减少。
2. 注意最大漏源击穿电压V<sub>BR(DSS)</sub>要大于供电电压，一般来说MOS的V<sub>BR(DSS)</sub>都能满足智能车需求。
   * 该款MOS为300V。
3. MOS管的开启时间t<sub>on</sub>和关断时间t<sub>off</sub>尽可能的短。

以上仅为部分MOS常见参数，还有最大栅源电压（这个参数是十分重要的，甚至可以说是MOS选型中最重要的一项参数，但是智能车一般都不会超过V<sub>GS</sub>）等等一些参数没有提及，有兴趣可以阅读芯片手册。

{% btn 'https://www.infineon.com/dgdl/Infineon-IPT004N03L-DS-v02_00-EN.pdf?fileId=db3a30433e9d5d11013e9e0f382600c2',IPT004N03L DATASHEET%}

## 驱动芯片选型

常见的半桥（全桥）驱动芯片`IR2184`、 `IR2104`、 `ISL6700`、 `MC33883`、 `HIP4082` 等。

其中关键的参数有但不限于<mark>导通关断时间</mark>、<mark>停滞时间（死区）</mark>、<mark>驱动电流</mark>等。经过多次比较分析芯片手册可知HIP以**200ns**的死区时间，**9ns**的导通关断时间等优越性能力压众多驱动芯片。

**具体参数详见芯片手册。**

### 自举电容：

![image-20200602173536672](http://img.pandior.ink/image-20200602173536672.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/I0VDQUQ5RQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

上图中C9、C11为自举电容，NMOS导通需要的条件是V<sub>GS</sub>大于开启电压V<sub>th</sub>，而上管Q1的源极S是浮地的，自举电容就是在浮地的基础上加压导通NMOS管。每次下桥臂的MOSFET开通时，通过该路径为电容器C充电。由于上桥臂器件的导通周期与电容器C中存储的电荷数量有特定关系，上桥臂的导通周期受限，无法在满占空比的情况下工作。

**与输出电压的情况一样，上桥臂的栅极电压波动使其对噪音很敏感。设计时需特别注意。**

具体流程：

当下管导通时，电源`12V`为电容进行充电，在下管关断，上管导通时又形成一条新的回路为上管加压可达到`12V+VBat`，保证导通。具体原理可自行上网查阅，或者假期我有时间再写一篇文章讲解。



自居电容的阻值计算可以通过以下公式得知：
$$
C\ge \frac{2[2Q_{g}+\frac{I_{qbs(max)}}{f} +Q_{ls}+\frac{I_{Cbs(leak)}}{f}] }{V_{cc}-V_{f}-V_{LS}-V_{Min}}
$$


+ Q<sub>g</sub>是促使开关管导通所需的栅极电荷量，查阅MOS手册可知
+ I<sub>qbs(max)</sub>是驱动芯片V<sub>BS</sub>最大静态电流，可以查阅驱动芯片手册得知
+ Q<sub>ls</sub>是每个周期电平转换所需要的电荷量，开关管低于500V时，一般小于5nC
+ I<sub>Cbs(leak)</sub>为电容的漏电流，f为开关频率
+ V<sub>f</sub>为自举二极管正向压降，这里选用的是肖特基二极管，压降很低一般0.2-0.4V
+ V<sub>LS</sub>为低侧开关管导通压降
+ V<sub>min</sub>为V<sub>b</sub>和V<sub>c</sub>之间最小电压

*经验总结：一般来说1uF的自居电容已经足够了，不行的话可以试着加大，10uF基本上留了很大的裕量*

## 栅极电阻

* 作用：其作用是调节MOSFET的开关速度，抑制尖峰电流，减少栅极出现的振铃现象,减小EMI, 也可以对栅极电容充放电起限流作用。该电阻的引入减慢了MOS管的开关速度,但却能减少EMI,使栅极稳定。

 **过大的栅极电阻会导致开关损耗增加，发热严重。**
 **较小的栅极电阻器会提高MOSFET的开关速度，易引发电压尖峰和振荡，从而造成器件故障和损坏。**
 ![image-20200602174706098](http://img.pandior.ink/image-20200602174706098.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/I0VDQUQ5RQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

 > EMI（Electromagnetic Interference）：电磁干扰。简单来说就是变化的磁场对周围电路会产生干扰（产生感生电动势等）进而影响电路正常工作，复杂PCB设计都要考虑EMI问题。

  > 振铃效应：是一种出现在信号快速转换时，附加在转换边缘上导致失真的信号。简单来说就是来回猛烈震荡并且逐渐衰减的信号。

![振铃效应](http://img.pandior.ink/image-20200529144454982.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/I0VDQUQ5RQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

## 栅极电阻并联二极管

*  作用：短路栅极电阻，减少放电时间。

![image-20200602174740853](http://img.pandior.ink/image-20200602174740853.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/I0VDQUQ5RQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

三极管包括MOS管在内的开关器件开启关断都需要一定的时间，分别记为开启时间t<sub>on</sub>和关断时间t<sub>off</sub>。

![IPT004N03L部分原理图](http://img.pandior.ink/image-20200529200825183.png?imageMogr2/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/I0VDQUQ5RQ==/dissolve/58/gravity/SouthEast/dx/20/dy/20|imageslim)

MOS管的关断时间要比开启时间慢得多，为了加快MOS的关断速度，可以在栅极电阻上反向并联一个二极管，当MOS管要关断时（栅极由高电动势降为低电动势）二极管导通，栅极电阻被短路从而有效降低电路阻抗，缩短放电时间。

