---
title: Notes of Razavi Electronics 1
date: 2021-12-05
updated: 2022-01-24
tags:
 - notes
categories:
 - IC
 - Electronics
keywords:
top_img: https://img.pandior.ink/north-star-2869817_1920.jpg
cover: https://img.pandior.ink/20211205202747.png
copyright_author: 
copyright_author_href: 
copyright_url: 
copyright_info: 
katex: true 
highlight_shrink: 
---

> This blog will record my learning experience for **Electronic 1**. And it will be a basic knowledge for my IC career.

<img src="https://img.pandior.ink/NJ8T}88GL]KD2IAI2VDKFRD.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

I will go through the red line to finish my study of MOS fundamental.

***<font color='red'>WHAT IS MORE!</font>  Each picture which is capture from razavi will be replace in my free time instead of disturbing the learning situation.*** 

# Basic Knowledge

## Modify carrier densities

### Doping

**N-type**

If we add $N_d$ <font color='red'>donor</font> atoms to semiconductors, then the density of free electrons is equal to $N_d$  per $cm^3$.

For pure $Si$ : $n=p=n_i$ , we could get $n*p={n_i}^2$

It also for doped $Si$ : $n*p={n_i}^2$

So for N-type $Si$ :   $n \approx N_d$, we could get $p \approx \frac{ {n_i} ^2} { N_d }$

- $n$: density of free electron (majority carrier)
- $p$: density of holes (minority carrier)

**P-type**

vice versa 

However, we call the boron atoms <font color='red'>acceptor</font>.  So if we add $N_a$ atoms per $cm^3$, we could get $N_a$ holes.

$p \approx N_a$, we could get $n \approx \frac{ {n_i} ^2} { N_a }$.

## Carrier Transport 

### Drift Current

the velocity of electron is that  $v=\mu_{n}E$,  $\mu_n$ is the <font color='red'>electron</font> mobility which equal with 1350 $(unit:\frac{m^2}{V\cdot s})$, $E$ is electric field which could be calculated by $E=\frac{V_B}{L}$

<img src="https://img.pandior.ink/QQ截图20211205200852.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 25%;" />

We could take this model as a example. The cuboid's width is $w$, length is $L$, height is $h$ and the volt of the battery is $V_B$.

So the total charge per second is $v*wh*nq=\left|I\right|=\mu_{n}\frac{V_B}{L}*wh*nq$, $n$ is the density of available electrons and $q$ is the charge of each electron 

AND we also have $R=\rho\frac{L}{w\cdot h}=\frac{V_B}{I}$

We can easy to get THAT
$$
R=\frac{L}{\mu_{n}whnq}=\frac{1}{\mu_{n}nq}\cdot \frac{L}{wh}=\rho\frac{L}{w h}
$$
NOW, we also could have the definition of <font color='red'>Current Density</font> $J_n=\mu_{n}Enq$ $(unit:\frac{A}{cm^2})$which could easy to know current without area. However, this formula is for ELECTRON. what about holes?

Total Current Density is that
$$
J=(\mu_{n}nq+\mu_{p}pq)*E
$$
In real application we usually forget one which is minority carrier.  

By the way, $\mu_{p}$ maybe 400 $(unit:\frac{m^2}{V\cdot s})$

### Diffusion Current

**definition**: movement of charge carrier from region of high concentration to region of low concentration 

<img src="https://img.pandior.ink/QQ截图20211206211950.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

Now, we have a formulation to describe the Current Density $J=D_{n}\frac{d_n}{d_x}q$, $D_{n}$ is diffusivity. 

*(you should also take a few of time to think about the sign of formulation, why it needn't negative? you'll find it's easy and right)*

When consider the holes and electrons, we could get the general formulation is that
$$
J_{total}=(D_{n}\frac{d_n}{d_x}-D_{p}\frac{d_p}{d_x})q,  (D_{n}=34cm^2/s;D_{p}=12cm^2/s)
$$

<img src="https://img.pandior.ink/QQ截图20211206211801.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 33%;" />

Q: Let's look at this plot. So why the current density decrease to zero with the $x$ axle growth. 

That is because electrons recombine with holes. If we have a n-type semi which was added large amount of donors, which means rare holes, what we could find is like the red line in the graph. 

### Einstein's Relation

We are curious about the relation between drift and diffusion. AND there also has a formulation that
$$
\frac{D}{\mu}=\frac{kT}{q},26mV@T=300K
$$
- $k$ is Boltzmann constant which is equal to $1.38064852 × 10^{-23} J/K$. 
- $T$ is absolute tempreture.

We also call this volt as <font color='red'>Thermal Voltage</font>. 

##  The PN Junction
### Quick Preview
**First of ALL, pn junction is not two piece silicon connected together. It's an integral piece of silicon with special craft.** <font color='red'>This is my first fault point along the time.</font>

<img src="https://img.pandior.ink/QQ截图20211206212108.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

There are two main different characters above. One is the negative of $V_x$ is different. The other is that the line isn't a straight line when the volt is positive. So what result to the strange thing? 

<img src="https://img.pandior.ink/QQ截图20211206211824.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

<font color='red'>Here is my next fault point.</font> The N or P type device's net charge is **neutral**. It is easy to understand. Just take the N-type semiconductor as an example, silicon atom is neutral and phosphorus atom is also neutral. HOW could the combination be negative?

<font color='red'>IMPOSSIBLE!!</font> If the phosphorus atom has a available electron, there also have a proton inside the nucleus. So does Silicon atom.

<img src="https://img.pandior.ink/QQ截图20211206211829.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

So, if we took a electron out of the material, we could have a positive iron.

### PN Junction in Equilibrium

<img src="https://img.pandior.ink/QQ截图20211208200833.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

So what happened in PN junction? 

First, it will have a diffusion. N-type silicon have a high concentration of electrons and the P-type silicon have low of that. For holes, vice versa .

With the process of diffusion, N-type silicon become positive and create a electric field which will preserve the diffusion. 

The highlight area is called <font color='red'>depletion region</font> where there are not any free electron. Because this area has depleted all free charge carrier.

**Equilibrium Condition**

<mark>Diffusion current of electrons = Drift current of electrons</mark>

<mark>Diffusion current of holes = Drift current of holes </mark>

Just take holes for example for quantitative analysis
$$
D_{p}\frac{d_p}{d_x}q=\mu_{p}pqE
$$
After eliminating $q$ and change some position of the equation, we integrate both sides, we get this


$$
\int D_{p}\frac{d_p}{p}=\mu_{p}\int E d_x
$$
We perform this integration from $x_1$ to $x_2$, so we can get this
$$
\int_{p_n}^{p_p} D_{p}\frac{d_p}{p}=\mu_{p}\int_{x_1}^{x_2} E d_x
$$
Solve the differential equation, the left side is easy. what we should pay attention is the electric field is not a  constant, it is a function with x. We don't care what is the function, we can deal it from the angle of physics.

$V_{AB}=-\int_{A}^{B}Ed_x$. 
$$
D_{p}\ln \frac{p_p}{p_n}=\mu_{p}\left [ V(x_1)-V(x_2) \right ]
$$
 the voltage of depletion region $V_0$ could be expressed that
$$
V_0=\frac{D_p}{\mu _p}ln \frac{N_aN_d}{n_i^2}
$$
due to the Einstein's Relation, we can also get this formula called Build-in Potential
$$
V_0=\frac{kT}{q}ln \frac{N_aN_d}{n_i^2}
$$

> There is no electric field outside the depletion region. We could prove it by Gauss's law. This also means that there is no voltage drop outside the depletion region.

Here are four observations:

1. Same $V_0$ expression is obtained if the electron current are considered.
2. If $N_a$ and $N_d$ are on the order of $10^{16}$ per cubic centimeter, $V_0$ may be 720 $mV$.
3. $V_0$ is localized. Because there is no electric field outside the depletion region.
4. We cannot measure $V_0$ from outside. 

> The reason for number 4 is that measuring $V_0$ requires that metal wires be attached from the device to a meter. It can be shown that the sum of the contact potentials at the interfaces from metal to P and at N to metal exactly cancel $V_0$. 

### PN junction in Reverse Bias

<img src="https://img.pandior.ink/QQ截图20211208222245.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

The polarity of battery to the opposed type of material. We call this as **reverse bias**. 

<font color='red'>The positive of battery will attract the electrons from N type semi, so the depletion region become **wider** in reverse bias.</font>

What is more interesting. We could consider PN junction as a capacitor. The left or right side could be considered as one plate because it has a good conductive quality like a metal. The depletion region just a insulator because it doesn't have any mobile charge in it. So the value of capacitor decrease in reserve bias. This device is called electronically- variable capacitor. "Varactor"

We have a formula to describe the relation about $C_j$, the capacitor of junction. The plot is below.
$$
C_j=\frac{C_{j0} }{\sqrt{1-\frac{V_R}{V_0}}} ,(V_R\le 0)
$$
<img src="https://img.pandior.ink/QQ截图20211208222251.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

### PN junction in Forward Bias

<img src="https://img.pandior.ink/QQ截图20211210130544.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

When the positive terminal of battery connect to the P-type of semi, vice verse, we call this bias as **forward bias**.

The holes of P-type semiconductor was pushed away by battery, vice verse. We allow the current to move forward.

We have a formula to describe the relation between current and voltage. The proof can be found in many book, and Razavi said we should put interest on circuit instead of proof because of time.
$$
I_{Junction}=I_s(\exp{\frac{V_x}{V_T}}-1)
$$

- $I_s:$  Reverse Saturation Current

- $V_T: \frac{kT}{q}$

<img src="https://img.pandior.ink/QQ截图20211210130640.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

If the $V_x$ is zero, the junction is in equilibrium so there has no current. 

When we give a reverse bias, it will have a very small current $I_s$, which depend on the density of donor and acceptor and the character of semiconductor. That is why we call it as **Reverse Saturation Current.** It more like a capacitor.
$$
I_s=A\cdot q\cdot n_i^2(\frac{D_n}{N_aL_n}+\frac{D_p}{N_dL_p})
$$

- $A:$ the cross section area of the diode (like resistor)
- $q:$ electron charge
- $n_i:$ related to material
- $D_n\space D_p:$ diffusivity of electrons and holes
- $N_a \space N_d:$ the doping density of electrons and holes
- $L_n\space L_p:$ diffusion lengths

> $A$ is so important that we should remember. It could be very large in power electronics where need large current or very small in integrated circuit.

At the positive of $V_x$, we will have a large current and it increases very quickly.

**Notes:**

1. If the forward bias voltage is $>4V_t$, we can make an approximation like $I_x=I_s \space exp{\frac{V_x}{V_T}}$. 

In practical applications, $V_x$ is usually on the order of 700 to 800 millivolts. So the number could be ignore.

2. If we know the value of current, we can use $V_x=V_T\ln{\frac{I_x}{I_s} }$

# Diode

## Quick View

<img src="https://img.pandior.ink/QQ截图20211210153253.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

**Definition:** a two-terminal device that carries current when it's voltage is positive and no current when it's voltage is negative.

<img src="https://img.pandior.ink/20211210135125.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

**From the two examples, wo can get a significant conclusion that the voltage goes up by 60 millivolts the current rises by a factor of 10.**

And the current is not so divergent, maybe a factor of 4 or 5. So we can make a approximation that the value of volts may be 700 or 800 millivolts. <font color='red'>**Typical forward bias voltages for diodes are in the range of 700-800 $mV$.** </font>

What's more, if a diode produced for large current, it's $I_s$ may be large.

## Modeling of PN junction

### Exponential Model (10-20%)

<img src="https://img.pandior.ink/QQ截图20211210154229.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

It is quite accurate model if we know $I_s$. But it always make trouble in calculation.

### Constant Voltage Model (70-80%)

<img src="https://img.pandior.ink/QQ截图20211212204045.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

If $V_x<V_{D,on}$ , diode off, like open circuit

If $V_x$ wants to exceed $V_{D,on}$ , diode on, like a battery.

$V_{D,on}:700-800mV$ 

### Ideal Diode Model (5-10%)

<img src="https://img.pandior.ink/QQ截图20211212204055.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

## Reverse Breakdown

<img src="https://img.pandior.ink/QQ截图20211212204104.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

We apply large enough volts, then the electric field is strong enough. And lots of electrons will leave their bonds and be free. so we get huge amount of current.

**The diode doesn't damage as long as the temperature isn't high.**

## Diode Applications

**Diode Models: exp, constant Voltage, ideal**

- All three models are nonlinear
- All three models distinguish between positive and negative ("rectification")
- The ideal model "passes" positive voltages, the constant voltage model passes voltages greater than $V_{D,on}$, and the exp model passes voltages **significantly** if $V_{D}>700-800$ $mV$

### Types of Characteristics

- I-V Characteristics

<img src="https://img.pandior.ink/QQ截图20211217221831.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

- Input-Output Characteristics

<img src="https://img.pandior.ink/QQ截图20211217221839.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

This two characteristics are what we are looking for when we analyze circuits.

### Simple Voltage Regulator

If a Bluetooth device need volts by 1.6V, and we have a battery which has 3V. There is a circuit designed for this.

<img src="https://img.pandior.ink/QQ截图20211219140722.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

The voltage across each diode is a weak function of its current. So the volts are very stable while the current of device is changing.

### Principles of Diode Circuit Analysis

1. Begin by assuming certain states for all diodes, check the final result again these assumptions.
2. If a diode is about to turn on or off, it must sustain a voltage of $V_{D,on}$ but its current is small.
3. If a diode is on and carries a current, the current must flow from the anode to the cathode.

## Practical Diode Circuits

- Rectifiers (chargers / adaptors)
- Limiters (FM receivers / optical communications)
- Voltage Doublers (RF receivers / flash memories)
- Level Shifts (General circuit)

 ### Basic Concepts

1. Analyze circuit to obtain: I-V char, input-output char. Also analyze by studying the **time response**.    <img src="https://img.pandior.ink/QQ截图20211220145105.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 33%;" />

2. Concept of "Tracking", eg, $V_{N}=V_{X}-V_{D,on}$, ($V_{N}$ tracks $V_X$, perhaps with a constant difference)

3. Quick review of capacitors ($I=C\frac{dV}{dt}$)

If we push current into the capacitor, the volts will grow up. Vice versa. 

<img src="https://img.pandior.ink/QQ截图20211220150537.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 33%;" />



### Half-Wave Rectifiers

Here is the circuit demonstration.

<img src="https://img.pandior.ink/QQ截图20211220152157.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

Firstly, we cloud analyze its I-V and Input-Output characteristics. We can see the $V_{out}$ tracks the $V_{in}$.

<img src="https://img.pandior.ink/QQ截图20211220152446.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 33%;" />

**Time Response**

We set the $V_{in}=V_osin\omega t$ , and see what is the output.

<img src="https://img.pandior.ink/QQ截图20211220154658.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

This is called **half wave rectifier**. Rectifier because it distinguishes between positive and negative inputs. Half wave because it allow half of the waveform to go to the output and block the other half of the waveform.

### Half-Wave Rectifiers with Smoothing Cap

The voltages could be given to laptop or any other device after Half-Wave Rectifiers because it isn't stable. We could use a low-pass filter (a resistor and a capacitor) after the circuit to extract DC power.

But what would happened if we just replace the resistor with a capacitor? We can try it.

<img src="https://img.pandior.ink/12.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 33%;" />

When the $V_{in}>V_{D,on}$, $D_1$ turn on. $V_{out}=V_{in}-V_{D,on}$, $V_{out}$ is pinned to $V_{in}$.

And when $V_{in}$ begins to decrease, $V_{out}$ will stay constant. WHY? First, the volts couldn't go up because the $V_{in}$ is lower than $V_{out}$ after peak. And more, it also couldn't go down. From what has been mentioned in number 3 of basic concepts, the volts couldn't decrease because the current couldn't through from cathode to anode.

Now, we rule out two possibilities. Staying constant has to be valid. The diode will keep turn off all the time. 

**Time Response**

<img src="https://img.pandior.ink/QQ截图20211221193854.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

We get a DC power without resistor and low-pass filter, just a smoothing capcitor.

**Reverse Voltage across D1**

The maximum reverse bias is $2V_{0}-V_{D,on}$.

**Two Points**

- Role of $R_1$ in the original  circuit?

<img src="https://img.pandior.ink/QQ截图20211220152157.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

 > Razavi: You need to ask yourself what is each device's function in every circuit, which will help you understand much better.

 Let's support a circuit without R1. When the D1 is off, we don't know the value of voltages because it isn't define. <font color='red'>So the purpose of R1 is to make sure that this voltage is in fact zero when D1 is off. In other word, here must be sth.</font>

 <img src="https://img.pandior.ink/QQ截图20211221204316.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

- Can we plot input-output Characteristics. for the rectifiers with Cap?

We can but we needn't. <font color='red'>In most situations, it make no sense and very complicated. </font>

From this formula $I=C\frac{dV}{dt}$, it is a function of **voltage** and **time**. We couldn't reflect **T** in the characteristics. It doesn't like former circuit, the output not only depend on input voltages but also the time. There is a storage element.

So we just research on **Time Response Characteristics**.

### Half-Wave Rectifiers with Cap and Load

<img src="https://img.pandior.ink/QQ截图20211221210315.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

Here is the circuit. We can make two extreme supports.

1. If the R1 is infinite, it likes HWR with cap. 

2. And if the value of cap is zero, the circuit just like the original HWR. 

So the waveform of output must like something between ***HWR*** and ***HWR* with Cap**.

**Time Response**

<img src="https://img.pandior.ink/QQ截图20211221212952.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

Before the peak, do the same analysis we have done many times. After the first peak, the diode turns off. The circuit can be simplified to something we are very familiar with.

<img src="https://img.pandior.ink/QQ截图20211221221546.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

> From the basic circuit theory, the $V_{out}$ will decay exponentially. 

So, as same as this simple circuit, $V_{out}$ decay exponentially too after peak. Before the second peak, $V_{in}$ come back and is more than $V_{out}$ plus $V_{D,on}$, the diode turn on. $V_{out}$ is pinned to $V_{in}$ again. What is following just like a circle.

This performance that the voltage goes up and down is called <font color='red'>**Ripple**</font>. Ripple is **undesirable** and we want a constant power supply for our devices. 

**How to decrease ripple?**

Now, we can make some approximations to simplify the analysis of ripple.

If the circuit is well designed, it means ripple has to be small. The decay has to be very slow and small. Here are two conclusions.

1. The decay lasts about one period of input ($T_{in}$). Because it decay very slowly and the time of diode turn on again is very close to the next peak. Just like a constant extremely.
2. exponential decay can be considered as linear decay



<img src="https://img.pandior.ink/QQ截图20211222151010.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 33%;" />

Why? we have a suppose that what is the waveform when the time duration much less than $\tau$.

Initial Voltage on $C_1=V_1$

If $t \ll \tau$, we can get 
$$
V_{out}=V_1\exp \frac{-t}{\tau}\approx V_1(1-\frac{t}{\tau})
$$
So we can approximate waveform by a straight line.

For ***HWR***, decay behavior like this: 
$$
V_{out}=(V_0-V_{D,on})(1-\frac{t}{\tau})
$$


take $t=T_{in}$ in
$$
V_{out}(t=T_{in})\approx (V_0-V_{D,on})(1-\frac{T_{in} }{\tau})
$$
the amplitude of ripple is that, $f_{in}$ is the input frequency
$$
V_{out}(t=0)-V_{out}(t=T_{in})=(V_0-V_{D,on})\frac{T_{in} }{\tau}=\frac{V_0-V_{D,on}}{R_1C_1f_{in} }
$$


*From this formula, if R1 is small, the ripple is large. Because the decay is faster, and that means we connect a heavier load which draw a lot of current.*

### Full-Wave Rectifiers 

Here is the Diode Bridge.

<img src="https://img.pandior.ink/QQ截图20211226174617.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

This time, we draw the Input-Output characterisetics from plus infinity to minus infinity.

Begin with $V_{in}$ very positive:

<img src="https://img.pandior.ink/QQ截图20211226175034.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

We could get $V_{out}$ by KVL:
$$
-V_{in}+V_{D,on}+V_{out}+V_{D,on}=0 \rightarrow V_{out}=V_{in}-2V_{D,on}
$$
If $V_{in}$ is sufficiently negative:

vice versa
$$
V_{out}=-V_{in}-2V_{D,on}
$$
<img src="https://img.pandior.ink/QQ截图20211226182141.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:33%;" />

### Full-Wave Rectifiers with Cap

![](https://img.pandior.ink/QQ截图20211226184356.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim)

The same analysis as HWR is. It will have a constant DC value.

### Full-Wave Rectifiers with Cap and Load

<img src="https://img.pandior.ink/QQ截图20211226190923.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

We should draw the time response of FWR with resister firstly.

<img src="https://img.pandior.ink/QQ截图20211226191112.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

The yellow line is easy to get and understand from the analysis of HWR. In the negative wave, it flips the negative cycles.

What the waveform like when we have both R1 and C1? From the study of HWR, we could draw it with the red line.

<img src="https://img.pandior.ink/QQ截图20211226192722.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

In full wave rectifier, the decay will last **half period of the input**. So from the formula of Ripple Amplitude,

$$
V_{out}(t=0)-V_{out}(t= \frac {T_{in} }{2})=\frac{V_0-2V_{D,on}}{R_1C_1f_{in} }*\frac{1}{2}
$$
**<font color='red'>So the amplitude of FWR is approximately 1/2 of HWR.</font>** We can say a full wave rectifier has about 1/2 ripple of a half wave rectifier when we have the same R1 modeling the load that draws a current, C1 and input frequency.

### Limiting Circuits

We can limit the swing of input wave.

<img src="https://img.pandior.ink/QQ截图20220105212837.jpg?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

### Voltage Doubler

**Observations**

1. To charge a cap. , we need to place positive charge on one plate and negative charge on the other.
2. the volt of this circuit will track the input, because it's impossible for a charge to come through from one plate to the other. In brief, the cap couldn't be charged, so it's volt is zero (original status) and then by KVL!<img src="https://img.pandior.ink/QQ截图20220112155004.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

3. the output of this circuit has a formulation with input $\frac {V_{out} }{V_{in} }=\frac {C_1}{C_1+C2}$ (By Laplace)<img src="https://img.pandior.ink/QQ截图20220112161630.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />
4. the output waveform like the blue line. In the first stage, the diode is on, and the capacitor is charged. After the first peak, we can use observation 2 to understand. The anode couldn't go down. If it keep constant, $C_1$ couldn't release charge because the direction of diode. So the voltage of anode decrease and the circuit is open.<img src="https://img.pandior.ink/QQ截图20220112164424.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim"  />

> **What is more. If we flip the diode, we could get the positive output.**

<img src="https://img.pandior.ink/QQ截图20220114234452.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

**Circuit and Analysis**

<img src="https://img.pandior.ink/QQ截图20220112172619.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

The left structure is observation 4 and the right one is part of half-wave rectifier.

<img src="https://img.pandior.ink/QQ截图20220115002822.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:80%;" />

This analysis is very complex and that is why push me away.

- IN STAGE Ⅰ

As the observation 4, $D_1$ was turn on and $C_1$ was charged. $D_2$ was turn off.

- IN STAGE Ⅱ

$D_2$ was turn on and $D_1$ was off. As the observation 3, the output would change $V_{out}$ because the input changed $2V_{out}$

- IN STAGE Ⅲ

The output keep constant. $D_1$ and $D_2$ were off. We could use the observation 2 to analyze.

- IN STAGE Ⅳ

As the circuit of stage Ⅰ, $C_1$ was charged. $D_1$ was turn on and $D_2$ was turn off.

- IN STAGE Ⅴ

As the circuit of stage Ⅲ. $D_1$ and $D_2$ were off. We could use the observation 2 to analyze.

- IN STAGE Ⅵ

$D_2$ was turn on and $D_1$ was off. As the observation 3, the output would change $\frac {V_{out} }{2}$ because the input changed $V_{out}$

So on...

Finally, the output will turn to a constant value that $2V_{out}$.

### Level Shift

<img src="https://img.pandior.ink/QQ截图20220115131118.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

  In some situations, we want to shift this signal up or down. So the shift circuit like this. The current source guarantee the diode is on and then we have a shift equaled to one diode drop. 

# MOSFETs

## Introduce

**observation**

<img src="https://img.pandior.ink/QQ截图20220116201007.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

The top plate is conductive material and the bottom plate is P-type semiconductor. These things build up a capacitor. 

The free charge carriers are equaled with $Q=C \cdot V_1$. 

- If $V_1 \uparrow \Longrightarrow Q\uparrow \Longrightarrow$electron density increases

- If $t \downarrow \Longrightarrow C \uparrow \Longrightarrow Q\uparrow \Longrightarrow$electron density increases

If $V_2$ is applied $\Longrightarrow$ current flours from A to B

If $V_1$ increases, electron density increases. $\Longrightarrow$ resistance between A and B $\downarrow \Longrightarrow$ current$\uparrow$

So we have made a  **voltage dependent current source** which we can use it to build amplifiers.

**MOS (Metal-Oxide-Semiconductor) structure**

<img src="https://img.pandior.ink/QQ截图20220116214730.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

1. The MOSFET(MOS Field effect transistor) has four terminals.
2. MOS structure is symmetric.

<img src="https://img.pandior.ink/QQ截图20220118110703.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

The current could be controlled by gate voltages.

**MOS Operation**

<img src="https://img.pandior.ink/QQ截图20220118191014.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

When the gate volts below the threshold voltage, the P-substrate just expose negative ions no electron.

When the gate volts exceed the threshold, the P-substrate brings free electron which can conduct current and form a **channel**.

As $V_G$ increases, electron density in the channel $ \uparrow  \Longrightarrow $ resistance between S and D $\downarrow$

### MOS Characteristics  

**Behavior of Channel**

case Ⅰ : $V_{GS} >V_{TH},V_S=V_D=0$

<img src="https://img.pandior.ink/QQ截图20220119103558.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 67%;" />

- Turned on, but has no current.
- The density of charge $Q=C\cdot V$

case Ⅱ : $V_{GS} >V_{TH},V_S=0,V_D>0$

<img src="https://img.pandior.ink/QQ截图20220119110217.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

- Here has a current.
- The density of charge $Q=C\cdot V$ we don't know. We just know the charge of channel decrease from S to D as the blue line because the channel is a resistor and has current.

**Dimensions of MOSFET**

<img src="https://img.pandior.ink/QQ截图20220119112007.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

quick note:

- In fabrication, we, designer, could just control the $W$ and $L$ except $t_{ox}$ which is decided by factory.

- The S and D region have a little overlap with the gate region because the thermal processing. So we have two length, one is L drawn which we design in the circuit and the other is L effective which we use in circuit analysis. <font color='red'>L effective will appear in our following equations.</font>

**Derivation of I/V characteristics**

- Channel Charge Density

case Ⅰ :  $V_{GS} >V_{TH},V_S=V_D=0$
$$
Q_{ch,total}=WL\cdot C_{ox}(V_{GS}-V_{TH}),unit:coulomb
$$
$C_{ox}:$ cap. per unit area     $unit:F/m^2$

$V_{GS}-V_{TH}$: overdrive voltage
$$
Q_{ch,density}=W\cdot C_{ox}(V_{GS}-V_{TH}),unit:coulomb/m
$$
case Ⅱ :  $V_{GS} >V_{TH},V_S=0,V_D>0$
$$
Q_{ch,density}=W\cdot C_{ox}[V_{GS}-V_{TH}-V(x) ],unit:coulomb/m
$$

- Drain Current

Before this part, we have a box with some formulation.

We can calculate the velocity of charge carrier under a electric field by  $v=\mu_{n}E$. (the velocity of electron is faster than hole. This equation has been mentioned above in Drift Current.) What's more, we know $E=-\frac{dV}{dx}$ in physic. So
$$
v=-\mu \frac{dV}{dx}
$$
<img src="https://img.pandior.ink/QQ截图20220119163043.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

Total charge in the blue length ($I_D$ has a reverse direction so the equation has a negative sign)
$$
I_D=-v\cdot Q_{ch,density}=-v\cdot W\cdot C_{ox}[V_{GS}-V_{TH}-V(x) ]
$$

$$
I_D=\mu_n \frac{dV}{dx}W\cdot C_{ox}[V_{GS}-V_{TH}-V(x) ]
$$

$$
\int_{0}^{L}I_D\cdot dx=\mu_n W C_{ox}\int_{0}^{V_{DS}}[V_{GS}-V_{TH}-V(x) ]\cdot dV
$$

$$
L\cdot I_D=\mu_n W C_{ox}[(V_{GS}-V_{TH})V-\frac{1}{2}V^2]_{0}^{V_{DS} }
$$

$$
I_D=\mu_n C_{ox} \frac {W}{L} [(V_{GS}-V_{TH})V_{DS}-\frac{1}{2}V_{DS}^2],V_{GS}>V_{TH}
$$

From the equation, if the $V_{GS}$ is constant, $I_D$ is a parabola function of $V_{DS}$. When $V_{DS}$ is equal to $V_{GS}-V_{TH}$, $I_D$ has a max value. What's more, when $V_{DS}$ is zero, the device hasn't current but a channel.

<img src="https://img.pandior.ink/QQ截图20220119182427.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

If $V_{DS}$ is constant, the graph likes this. Only when $V_{GS}>V_{TH}$, the equation could be right.

<img src="https://img.pandior.ink/QQ截图20220119182437.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

**I/V Characteristics**

From the equation $I_D=\mu_n C_{ox} \frac {W}{L} [(V_{GS}-V_{TH})V_{DS}-\frac{1}{2}V_{DS}^2],(V_{GS}>V_{TH} )$, we could found If $V_{DS}\ll 2(V_{GS}-V_{TH})$, we could get $I_D\simeq \mu_n C_{ox} \frac {W}{L}(V_{GS}-V_{TH})V_{DS}$.

$I_D$ is linearly dependent on $V_{DS}$ or $V_{GS}$. If we keep $V_{GS}$ constant, now, MOS device acts as a linear resistor. 

<img src="https://img.pandior.ink/QQ截图20220124145656.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 50%;" />

$R_{on}=\frac{1}{\mu_n C_{ox} \frac {W}{L}(V_{GS}-V_{TH})}$ the value of res could be adjusted by $V_{GS}$, so it is a electronically adjustable resistor. 

- A MOSFET can act as a voltage-dep. resistor if $V_{DS}\ll 2(V_{GS}-V_{TH})$.

- MOS device as a Switch

<img src="https://img.pandior.ink/QQ截图20220124150644.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:67%;" />

- $I_D$ for $V_{DS}>V_{GS}-V_{TH}$?

In this situation, the point that $V_{DS}=V_{GS}-V_{TH}$  couldn't create electrons and build a channel which we call **pinch off**.

<img src="https://img.pandior.ink/QQ截图20220124154546.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

And with $V_{DS}$ increasing, the point move left very slowly. It's a very weak function. **So The total length of channel doesn't change much.**

**Rederive the I/V equation**

If the MOS has pinched off, we have  
$$
\int_{0}^{L}I_D\cdot dx=\mu_n W C_{ox}\int_{0}^{V_{GS}-V_{TH} }[V_{GS}-V_{TH}-V(x) ]\cdot dV
$$
So
$$
I_D=\frac {1}{2}\mu_n C_{ox} \frac {W}{L} (V_{GS}-V_{TH})^2,(V_{GS}>V_{TH},V_{DS}\ge V_{GS}-V_{TH})
$$
and we also have this equation above
$$
I_D=\mu_n C_{ox} \frac {W}{L} [(V_{GS}-V_{TH})V_{DS}-\frac{1}{2}V_{DS}^2],(V_{GS}>V_{TH},V_{DS}\le V_{GS}-V_{TH})
$$



So we have two distinct regions of operation. Triode & Saturation Region.

<img src="https://img.pandior.ink/QQ截图20220124163153.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom: 67%;" />

If $V_{DS}$ is much large, we have a constant current source.

<img src="https://img.pandior.ink/QQ截图20220124163537.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

**$I_D-V_{GS}$ characteristic**

<img src="https://img.pandior.ink/QQ截图20220124164919.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />

The MOS device always turns on in saturation if $V_{DS}>0$.

**Simple Model**

Saturation

<img src="https://img.pandior.ink/QQ截图20220124164926.png?imageMogr2/auto-orient/format/png/blur/1x0/quality/100|watermark/2/text/cGFuZGlvci5pbms=/font/dmlqYXlh/fontsize/1760/fill/IzdFOEM4QQ==/dissolve/65/gravity/SouthEast/dx/20/dy/20|imageslim" style="zoom:50%;" />















