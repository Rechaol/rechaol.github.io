# 计算机组成
好吧，今天终于开始写这个模块了。虽然很简单的知识总结，但是可能这只是给我自己看的。
其实我也没有想好到底写个什么开头，就记录个开头吧。谢谢！
## brief introduction
Pre-computer – ~ 1946
Non-electrical, non-programmable (非电子，不可编程)

First Generation – 1946 ~ 1956
Vacuum tubes, programmable (电子管，可编程，图灵完全)

Second Generation – 1956 ~ 1964
Transistor, programming languages (晶体管，编程语言开始应用)

Third Generation – 1964 ~ 1971
Integrated Circuit, OS (集成电路，操作系统开始应用)

Fourth Generation – 1971 ~ now
Microprocessor, GUI, Personal Computer
(大规模集成微处理器, 图形用户界面, 个人电脑兴起)

Fifth Generation – future

This is the brief introduction of the history of the development of the computer.As we all know,the first computer in our common sense is ENIACS(1946) which at that time is really exellent.(It's said that even some computing work of the first atomic bomb is done on this computer.)Before that machine was made by US military,John von Neomann announced that one structure of the computer is to seperate the computation and memory which is called as the structure of von Neumann(1945).However ENIACS isn't based on this structure,probably because this structure is too late for ENIACS.But until now the most advanced computer is based on this structure.

Then with the development of the transistor technology,the use of transistor deeply changes the computer,including the coverage of the computer.And now we are still using the number of transistors to judge whether the CPU is advanced or not.As the development of the technology and the material,more and more transistors can be placed on the per unit area.So now the most famous law is got.Moore's law tells that every 18 to 24 months the number of transistors placed on per unit area will be as twice large as before.However now this law is breaking down.

Now we have known the development of the computer.So what is a computer?How can we define one thing as computer?

The definition of the computer is an electronic device that manipulates data according to a list of instructions (program), with capability of Turing machine.In this definition,we can find four key parts in this definition-an electronic device,have a list of instructions,manipulate data,capability of Turing machine.This term we will learn about the component of the CPU and the solution now the world takes to solve memory gap and power gap problem.

## chapter1 the preformance of the CPU
First let we define the performance of the CPU.Performance of the CPU is equal to the reciprocal of the execution time.So when we notice that A is n time faster than B,we consider that the n is equal to the execution time of B divided by that of A.

Now we will define some common concept.

CPU time:time spent processing a given job

Clock period:duration of a clock cycle

Clock frequency:cycles per second

(The two concepts are reciprocal of each other.)

CPU time=clock cycle * cycle time=clock cycle/clock rate;

CPI:the full name of CPI is cycle per instruction

CPU time=instruction count * CPI * cycle time=instruction count * CPI/clock rate

When we have an instruction set which has different types of instructions,we can count the average CPI.

MIPS:million instructions per second

MIPS=clock rate/(CPI*10^6)

The last thing in this chapter is Amdahl's law.Improving an aspect of a computer and expecting a proportional improvement in overall performance isn't really affecting.

## eight design laws
Design for Moore’s Law （设计紧跟摩尔定律）

Use Abstraction to Simplify Design (采用抽象简化设计)

Make the Common Case Fast (加速大概率事件)

Performance via Parallelism (通过并行提高性能)

Performance via Pipelining (通过流水线提高性能)

Performance via Prediction (通过预测提高性能)

Hierarchy of Memories (存储器层次)

Dependability via Redundancy (通过冗余提高可靠性)

