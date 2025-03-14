<!-- .slide: style="text-align: left;"> -->  
# Adder
By YSYX-Tmmo
----

## What is adder?
--

<!-- .slide: style="text-align: left;"> -->  
### A simple Adder
C++:
``` c++
sum = a + b;
```
Verilog:
``` Verilog
assign sum = a + b;
```
ASM:
```asm
add a0, a1, a2
```
--

<!-- .slide: style="text-align: left;"> -->  
### in logisim

![HA](assets/Adder/HA.png)
--

<!-- .slide: style="text-align: left;"> -->  
For "add" still need carry out, so:
```Verilog
sum  = a ^ b
cout = a & b
```
![HA1](assets/Adder/HA1.png)

But it only can add one bit
----

<!-- .slide: style="text-align: left;"> -->  
## How to add more bit in circuit?
series adder
--

<!-- .slide: style="text-align: left;"> -->  
### Full Adder
- HA can only output carry
- FA should handle the carry from last adder
![FA](assets/Adder/FA.png)
--

<!-- .slide: style="text-align: left;"> --> 
### How much time it takes?
- Define one gate need 1 delay time（1d）
- D(x) : the delay time of x
- eg: $D(FA_c) = 3d$
![FAD](assets/Adder/FAD.png)
--

<!-- .slide: style="text-align: left;"> --> 
### Ripple-Carry Adder 
![RCA](assets/Adder/RCA.png)
- $D(RCA_c)=12d$ or $D(RCA_c)=9d$ ? 
- Can it be fater?
----

<!-- .slide: style="text-align: left;"> --> 
## observe
- $D(cout)=3d$
- $D(sum)=2d$
![FAD](assets/Adder/FAD.png)
--

<!-- .slide: style="text-align: left;"> --> 
## observe
For FA
- $cout = ((a ^ b) & cin) | (a & b)$
- $sum = a ^ b ^ cin$

For RCA 
- $Cout_0 = ((a_0 ^ b_0) & cin) | (a_0 & b_0)$
- $Cout_1 = ((a_1 ^ b_1) & cout_0) | (a_1 & b_1)$
- $Cout_2 = ((a_2 ^ b_2) & cout_1) | (a_2 & b_2)$
- $Cout_3 = ((a_3 ^ b_3) & cout_2) | (a_3 & b_3)$
--

<!-- .slide: style="text-align: left;"> --> 
## observe
Define
- $G = a & b$
- $P = {a} $^$ {b}$

$$
Cout_1 = ((a_1 ^ b_1) & (((a_0 ^ b_0) & cin) | (a_0 & b_0))) | (a_1 & b_1)
Cout_3 = ((a_3 ^ b_3) & (((a_2 ^ b_2) & (((a_1 ^ b_1) & 
           (((a_0 ^ b_0) & cin) | (a_0 & b_0))) | (a_1 & b_1))) | 
           (a_2 & b_2))) | (a_3 & b_3)
$$
--

<!-- .slide: style="text-align: left;"> --> 
## observe
$$
Cout_1 = ((a_1 ^ b_1) & (((a_0 ^ b_0) & cin) | (a_0 & b_0))) | (a_1 & b_1)
Cout_3 = ((a_3 ^ b_3) & (((a_2 ^ b_2) & (((a_1 ^ b_1) & 
           (((a_0 ^ b_0) & cin) | (a_0 & b_0))) | (a_1 & b_1))) | 
           (a_2 & b_2))) | (a_3 & b_3)
$$