
# Chisel Open Source


## 1. What is Chisel?

[Chisel](https://github.com/chipsalliance/chisel3) is a hardware design language that facilitates advanced circuit generation and design reuse for both ASIC and FPGA digital logic designs. Chisel adds hardware construction primitives to the Scala programming language, providing designers with the power of a modern programming language to write complex, parameterizable circuit generators that produce synthesizable Verilog. This generator methodology enables the creation of re-usable components and libraries, such as the FIFO queue and arbiters in the Chisel Standard Library, raising the level of abstraction in design while retaining fine-grained control.

For more information on the benefits of Chisel see: ["What benefits does Chisel offer over classic Hardware Description Languages?"](https://stackoverflow.com/questions/53007782/what-benefits-does-chisel-offer-over-classic-hardware-description-languages)

Chisel is powered by [FIRRTL](https://github.com/chipsalliance/firrtl) (Flexible Intermediate Representation for RTL), a hardware compiler framework that performs optimizations of Chisel-generated circuits and supports custom user-defined circuit transformations.

#### To be short, Chisel is a tool for generating verilog using Scala

#### Scala is almost same with kotlin, they have so many overlapping points in the view of grammar, coding style, and so on. so Chisel can be easy way to generate Hardware RTL for Software engineer


## 2. What does this page guide for?

this repository is a guide for open library [gradleRocketchip](https://github.com/yoonhyeonjoon/gradleRocketchip)

gradleRocketchip includes utilized Chisel codes and example codes to understand this grammar. but the modules made without elaborated considering of packaging, so it is some clumsy.   

the Lec pages of this repository would be help to approach the gradleRocketchip. 

and if you are not familiar with basic theories and grammar of Scala, this [github(agile-hw)](https://github.com/agile-hw/lectures/) will be helpful!!  

## 3. Lecture Link

<br>

[Lec 01 - RocketChip build guide to generate Verilog](lec01-SettingGuide.md)
<br><br>
[Lec 02 - Build file and Check the wave form using AysncQueue Example](lec02-AsyncQueue.md)
<br><br>
[Lec 03 - Code Following using Queue Example ](lec03-Queue.md)



<br>
<br>
<br>
<br>

