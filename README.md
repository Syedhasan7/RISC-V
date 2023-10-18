# Building a RISCV Core
This repository contains all the information regarding the 5-day RISC-V based CPU Core Design MYTH (Microprocessor for You in Thirty Hours) Workshop, offered by for VLSI System Design (VSD) and Redwood EDA.
The RISC-V CPU Core has been designed with the help of Transaction Level Verilog(TL-Verilog) in addition with the Makerchip IDE Platform. 
# TL-Verilog
Transaction-Level Verilog (TL-Verilog) is an emerging extension to SystemVerilog that supports a new design methodology, called transaction-level design. For this project, TL-Verilog has been chosed as the HDL of choice for the design. Projects on Makerchip can be completely designed using TL-Verilog. Transaction Level Verilog standard is an extension of Verilog which has various advantages like simpler syntax, shorter codes and easy pipelining. Tha main advantage of TL-Verilog over System Verilog is the amount of code reduction in designing even a simple model.
# INSTALLATION
For installation and more details regarding iverilog, yosys and gtkwave, refer to :

https://github.com/Veda1809/pes_asic_class

This repo mainly focuses on Day3-5.

# TABLE OF CONTENTS
## DAY 1 
**Introduction to RISCV ISA and GNU Compiler Toolchain**
+ [Introduction to Basic Keywords](#introduction-to-basic-keywords)
+ [Labwork for RISCV Toolchain](#labwork-for-riscv-toolchain)
+ [Integer Number Representation](#integer-number-representation) 
  
## DAY 2 
**Introduction to ABI and Basic Verification Flow**
+ [Application Binary Interface](#application-binary-interface)
+ [Labwork using ABI Function Calls](#labwork-using-abi-function-calls)

## DAY 3
**Digital Logic with TL-Verilog and Makerchip**  
+ [Combinational Logic in TL-Verilog using Makerchip](#combinational-logic-in-tl-verilog-using-makerchip)
+ [Sequential Logic](#sequential-logic)
+ [Pipelined Logic](#pipelined-logic)
+ [Validity](#validity)

## DAY 4
**Basic RISC-V CPU Microarchitecture**
+ [Introduction](#introduction)
+ [Fetch and Decode](#fetch-and-decode)
+ [RISC-V Control Logic](#risc-v-control-logic)

## DAY 5
**Complete Pipelined RISC-V CPU Micro-architecture**
+ [Pipelining the CPU](#pipelining-the-cpu)
+ [Solutions to Pipeline Hazards](#solutions-to-pipeline-hazards)
+ [Load & Store Instructions and Completing RISC-V CPU](#load-&-store-instructions-and-completing-risc-v-cpu)
+ [Wrap up](#wrap-up)

# Day-1   
## Introduction to Basic Keywords
<details>
<summary> Introduction </summary>
	
- **ISA (Instruction Set Archhitecture)**
  - ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.
  - It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.

- **RISC-V (Reduced Instruction Set Computing - Five)**.
  - It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
  - RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions. 

<img width="536" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4eabe0b7-4581-419b-88e7-84c7ac1dac8e">

</details>

<details>
<summary> From Apps to Hardware </summary>

1. **Apps:** Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.
2. **System software:** System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'
3. **Operating System:** The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

4. **Compiler:** A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

5. **Assembler:** An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

6. **RTL:** RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

 7. **Hardware:** Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

</details>

<details>
<summary> Detail Description of Course Content </summary>

**Pseudo Instructions:** Pseudo-instructions are used to simplify programming, improve code readability, and reduce the number of explicit instructions a programmer needs to write. They are especially useful for common programming patterns that involve multiple instructions.
`Ex: li, mv`.

**Base Integer Instructions:** The term "base integer instructions" refers to the fundamental set of instructions that form the foundation for performing basic arithmetic, logical, and data movement operations.
`Ex: add, sub, and, or, xor, sll`.

**Multiply Extension Intructions:** The RISC-V architecture includes a set of multiply and multiply-accumulate (MAC) extension instructions that enhance the instruction set to perform efficient multiplication and multiplication-accumulate operations.
`Ex: mul, mulh, mulhu, mulhsu`.

**Single and Double Precision Floating Point Extension:** The RISC-V architecture includes floating-point extensions that provide support for both single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations. These extensions are often referred to as the "F" and "D" extensions, respectively. Floating-point arithmetic is essential for handling real numbers with fractional parts and for performing accurate calculations involving decimal values.

**Application Binary Interface:** ABI stands for "Application Binary Interface." It is a set of rules and conventions that govern how software components interact with each other at the binary level. The ABI defines various aspects of program execution, including how function calls are made, how parameters are passed and returned, how memory is allocated and managed, and more.

**Memory Allocation and Stack Pointer** 
- Memory allocation refers to the process of assigning and managing memory segments for various data structures, variables, and objects used by a program. It involves allocating memory space from the system's memory pool and releasing it when it is no longer needed to prevent memory leaks.
- The stack pointer is a register used by a program to keep track of the current position of the program's execution on the call stack. 

</details>

## Labwork for RISCV Toolchain

<details>
<summary> C Program </summary>

+ We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.

`leafpad sumton.c`
``` c
#include<stdio.h>

int main(){
	int i, sum=0, n=111;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}
```
<img width="345" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2d5e3fe1-f8fd-434b-8faf-2912d3c056e1">

+ Using the gcc compiler, we compiled the program to get the output.

`gcc sumton.c`
`.\a.out`

<img width="545" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/0b7e7911-d0b2-4a6a-aefd-cd9b4d520a4f">

</details>

<details>
<summary> RISCV GCC Compiler and Dissemble </summary>

+ Using the riscv gcc compiler, we compiled the C program.

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`

+ Using `ls -ltr sum1ton.c`, we can check that the object file is created.

+ To get the dissembled ALP code for the C program, 

`riscv64-unknown-elf-objdump -d sum1ton.o | less` .

+ In order to view the main section, type 
   - `/main`
   - press ENTER
   - press `n` to search next occurance
   -  press `N` to search for previous occurance

+ Here, since we used -O1 optimisation, the number of instructions are 15.

<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/98843b92-0beb-4bfc-ba4b-1dac5c93ed3c">

+ When we use -Ofast optimisation, we can see that the number of instructions have been reduced to 12.

<img width="422" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3eb7afcd-0645-4340-bcac-ae2dc3258ce3">

   - -Onumber : level of optimisation required
   - -mabi : specifies the ABI (Application Binary Interface) to be used during code generation according to the requirements
   - -march : specifies target architecture

+ In order to view the different options available for these fields, use the following commands

 go to the directory where riscv64-unkonwn-elf is present

  - -O1 : ``` riscv64-unkonwn-elf --help=optimizer```
  - -mabi : ```riscv64-unknown-elf-gcc --target-help```
  - -march : ```riscv64-unknown-elf-gcc --target-help```

+ To quit:
  - use ```esc :q``` to quit

</details>

<details>
<summary> Spike Simulation and Debug </summary>

+ `spike pk sum1ton.o` is used to check whether the instructions produced are right to give the correct output.

<img width="523" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2fa7d825-102f-41ed-b9e6-a31c2417cb22">


+ `spike -d pk sum1ton.c` is used for debugging.

+ The contents of the registers can also be viewed.

<img width="317" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/be6fcaa9-ab93-46e0-8da3-7b8056d09f0c">

   - press ENTER : to show the first line and successive ENTER to show successive lines
   - reg 0 a2 : to check content of register a2 0th core
   - q : to quit the debug process

</details>

## Integer Number Representation 

<details>
<summary> Unsigned Numbers </summary>

- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
- Range: [0, (2^n)-1 ]

</details>

<details>
<summary> Signed Numbers </summary>

- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
- Range :
   - Positive : [0 , 2^(n-1)-1]
   - Negative : [-1 to 2^(n-1)]

</details>

<details>
<summary> Labwork </summary>

+ We wrote a C program that shows the maximum and minimum values of 64bit unsigned numbers.

``` c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```
<img width="531" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1195a00a-9b42-4a33-bce0-6095e5350647">


+ We wrote a C program that shows the maximum and minimum values of 64bit signed numbers.
``` c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```
<img width="481" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/48c4c465-8324-4765-98fe-20584143f33f">

</details>

# Day-2
## Application Binary Interface

<details>
<summary> Introduction to ABI </summary>

+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.

</details>

<details>
<summary> Memory Allocation for Double Words </summary>

64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly
1. **Little-Endian:**
In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. **Big-Endian:**
In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
#### For example, consider the 64-bit hexadecimal value 0x0123456789ABCDEF. 
In Little-Endian representation, it would be stored as follows in memory:

<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8c63e751-8882-4b1e-a2f8-84da628ee604">


In Big-Endian representation, it would be stored as follows in memory:

<img width="454" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3954540e-800f-4503-97ef-6c77daacd058">

</details>

<details>
<summary> Load, Add and Store instructions </summary>

Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.

Example `ld x6, 8(x5)`

In this Example
- `ld` is the load double-word instruction.
- `x6` is the destination register.
- `8(x5)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x8, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x8` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x9` is the destination register.
- `x10` and `x11` are the source registers.

</details>

<details>
<summary> 32-Registers and their ABI Names </summary>

The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.
#### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components. 

<img width="430" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3b7aed64-37cd-492f-b9b5-cd840103566a">

</details>

## Labwork using ABI Function Calls

<details>
<summary> Algorithm for C Program using ASM </summary>

- Incorporating assembly language code into a C program can be done using inline assembly or by linking separate assembly files with your C code.
- When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
- The program executes the assembly function, following the assembly instructions you've provided.
<img width="477" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/6afb1381-2237-46b0-831a-984e73e1e289">

</details>

<details>
<summary> Review ASM Function Calls </summary>

- We wrote C code in one file and your assembly code in a separate file.
- In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.

**C Program**
`custom1to9.c`
  ``` c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
```
**Asseembly File**
`load.s`
``` s
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```

</details>

<details>
<summary> Simulate C Program using Function Call </summary>

+ **Compilation:** To compile C code and Asseembly file use the command

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o custom1to9.o custom1to9.c load.s` 

this would generate object file `custom1to9.o`.

+ **Execution:** To execute the object file run the command 

`spike pk custom1to9.o`

<img width="517" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/46d311ec-4bf9-4ad8-b758-b39eef1dbc7c">

</details>

<details>
<summary> Lab to Run C-Program on RICV-CPU </summary>


+ `git clone https://github.com/kunalg123/riscv_workshop_collaterals.git`

+ `cd riscv_workshop_collaterals`

+ `ls -ltr`

+ `cd labs`

+ `ls -ltr`

+ `chmod 777 rv32im.sh`

+ `./rv32im.sh`

<img width="517" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/16c15f04-b5c9-441f-9b87-f9e35b19dc6f">

</details>

# Day-3
## Combinational Logic in TL-Verilog using Makerchip
<details>
<summary> Introduction </summary>

+ **Logic Gates**
  
  Logic gates are fundamental building blocks of digital circuits and are used to perform logical operations on binary numbers. They manipulate binary information, where 0 represents false or low voltage, and 1 represents true or high voltage.

<p align="center">
<img width="505" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/dc4c7ced-363f-4712-9ffd-d52da2a217bf">
</p>
<p align="center">
  Fig 1.
</p>

+ **Boolean Operation**

  Boolean operations are fundamental operations in Boolean algebra, a mathematical structure dealing with variables that can take on one of two values, typically denoted as true (1) and false (0).

<p align="center">
<img width="344" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/6d87e1de-cd86-4708-89e5-d8f14c84c5de">
</p>
<p align="center">
  Fig 2.
</p>

+ **Basic Mux Implementation**

   A 2:1 multiplexer (also known as a 2-to-1 mux) is a digital circuit that selects one of two input data lines and directs it to a single output line based on a control signal. The control signal determines which of the two input lines is transmitted to the output.

<p align="center">
<img width="167" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5d858058-d4b0-4e6e-ad53-d402aab85f7c">
</p>
<p align="center">
  Fig 3.
</p>

``` v
assign f = s ? x1 : x2;
```

+ **Chaining Ternary Operator**

<p align="center">
<img width="151" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c478b402-a4d2-4bd9-b883-c25bd5c58197">
<img width="157" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/2682bfab-f2b8-4c4a-a90f-e6db6f6c4ac2">
</p>
<p align="center">
  Fig 4.
</p>

```v
assign f = sel[0] ? a : (sel[1] ? b : (sel[2] ? c : d)) ;
```

</details>

<details>
<summary> Makerchip Platform </summary>

Makerchip is a free online environment by Redwood EDA for developing high-quality integrated circuits. The online platform can be used to code, compile, simulate and debug Verilog designs from a browser. It gives you a place to create any digital sequential logic you can dream up faster than you ever thought was possible, all within your browser. 

+ Go to http://makerchip.com/
+ Click `IDE`
+ Open `Tutorials` then `Validity Tutorial`
+ Click `Load Pythogorean Example`
+ Split planes and move tabs.
+ Zoom/pan in Diagram with mouse wheel and drag.
+ Zoom waveform with `Zoom In` button.
+ Click `$bb_sq` in waveform to highlight in the diagram.

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/351ab7e6-940b-47c4-9a06-d687d99147f3">
</p>
<p align="center">
  Fig 5.
</p>

</details>

<details>
<summary> Labs </summary>

**Inverter**
+ Open `Examples`(under `Tutorials`).
+ Load `Makerchip Default Template`.
+ Make an inverter.
+ On line 16, in place of `//..` , type `$out = ! $in1;` (preserve 3-space indentation, no tabs).
+ Compile (`E` menu).

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/afa6bd69-0e70-4ca6-b5a0-4e5d1a5b12fd">
</p>
<p align="center">
  Fig 6.
</p>

  + There was no need to declare $out and $in1 unlike verilog, and no need to assign $in1 . Random stimulus is generated and a warning is produced.


**OR**
+  On line 16, in place of `//..` , type
  ```v
  $out = $in1 | $in2;
  ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f6cacef7-f094-4e85-950c-2f8c52896250">
</p>
<p align="center">
  Fig 7.
</p>

**Vectors**
+ Arithmetic operations operate on vectors as binary numbers.
+  On line 16, in place of `//..` , type

 ```v
  $out[4:0] = $in1[3:0] + $in2[3:0];
```

+  `$out[4:0]` creates a vecot of 5 bits.

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e7f72dc9-45d7-41b2-8194-1846c454065b">
</p>
<p align="center">
  Fig 8.
</p>

**MUX**
+ ```v
  $out = $sel ? $in1 : $in2;
  ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/87170d58-c4d6-4a59-9f4c-d23d9812698d">
</p>
<p align="center">
  Fig 9.
</p>

+ Modified the mux to operate on vectors.
   - ```v
     $out[7:0] = $sel ? $in1[7:0] : $in2[7:0];
     ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f32f865a-3f6e-4f32-82c2-ca3af28b6c7e">
</p>
<p align="center">
  Fig 10.
</p>

**Combinational Calculator**

<p align="center">
  <img width="308" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c28c7768-d70f-4bb0-8bc4-e96a78267add">
</p>
<p align="center">
  Fig 11.
</p>

```v
$reset = *reset;
$val1[31:0] = $rand1[3:0];
$val2[31:0] = $rand2[3:0];
$sum[31:0] = $val1[31:0] + $val2[31:0];
$diff[31:0] = $val1[31:0] - $val2[31:0];
$prod[31:0] = $val1[31:0] * $val2[31:0];
$quot[31:0] = $val1[31:0] / $val2[31:0];
$out[31:0] = $op[1] ? ($op[0] ? $quot : $prod)
                    : ($op[0] ? $diff : $sum);
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/b085c8d7-b712-4625-80bf-c9d2bbdc93c0">
</p>
<p align="center">
  Fig 12.
</p>

</details>

## Sequential Logic
<details>
<summary> Introduction </summary>

**Sequential Logic**
+ Sequential logic is sequenced by a clock signal.
+ A D-FF transitions next state to current state on a rising clock edge.
+ The circuit is constructed to enter a known state in response to a reset signal.

<p align="center">
<img width="265" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/b4e2e060-11f2-4d37-92a1-f0118c97f10d">
</p>
<p align="center">
  Fig 1.
</p>

**Values in Verilog**
<p align="center">
  <img width="281" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e220d1be-1f0f-4cd2-ae27-6a12e73c77ab">
</p>
<p align="center">
  Fig 2.
</p>

+ Simulator configuration :
  - will zero-extend or truncate when widths are mismatched (without warning).
  - uses 2-state simulation (no X's)
</details>

<details>
<summary> Labs </summary>

**Fibonacci Series-Reset**

+ Next value is the sum of previous two numbers: 1, 1, 2, 3, 5, 8, ...
<p align="center">
<img width="247" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/d3998208-dfb3-4375-ab65-3abc633819ac">
</p>
<p align="center">
Fig 3.
</p>

+ ```v
  $num[31:0] = $reset ? 1 : (>>1$num + >>2$num);
  ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/1aeae6a6-4ff7-45c0-8897-b110e5b30c57">
</p>
<p align="center">
Fig 4.
</p>

**Counter**

+ Designed a free running counter.

<p align="center">
<img width="143" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/20c5e180-cb88-4a52-9bfd-f45a8e4f4033">
</p>
<p align="center">
  Fig 5.
</p>

+ ```v
     $cnt[31:0] = $reset ? 0 : (1 + >>1$cnt);
  ```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7f492f6d-24aa-48e6-8a37-a2836264f251">
</p>
<p align="center">
  Fig 6.
</p>

**Sequential Calculator**

<p align="center">
<img width="314" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/b1c50abb-e7e8-4f01-8973-093a02c26cbe">
</p>
<p align="center">
  Fig 7.
</p>

+ ```v
   $reset = *reset;
   $val2[31:0] = $rand2[3:0]; 
   $val1[31:0] = >>1$out[31:0];
   $sum[31:0] = $val1[31:0] + $val2[31:0];
   $diff[31:0] = $val1[31:0] - $val2[31:0];
   $prod[31:0] = $val1[31:0] * $val2[31:0];
   $quot[31:0] = $val1[31:0] / $val2[31:0];
   $out[31:0] = $reset ? 32'b0 :
                ($op[1] ? ($op[0] ? $quot : $prod)
                        : ($op[0]? $diff : $sum));
  ```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5576c9d8-d46e-407a-8473-b2027fe06cee">
</p>
<p align="center">
  Fig 8.
</p>

<p align="center">
<img width="540" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e2b63305-29bf-41a6-8073-3ac5b504f684">
</p>
<p align="center">
  Fig 9.
</p>

</details>

## Pipelined Logic
<details>
<summary> Introduction </summary>

**Pythagoras's Theorem**

<p align="center">
  <img width="151" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/72828588-2914-46a1-9cc6-22e36ab47151">
</p>
<p align="center">
  Fig 1.
</p>

+ Computation cannot be done in a single cycle, hence we distribute the calculation over 3 cycles.
<p align="center">
  <img width="298" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/d03e696c-fd46-446b-9c44-995806260706">
</p>
<p align="center">
  Fig 2.
</p>

+ TL Verilog gives us the ability to model this in what we called as **timing abstract** representation.
<p align="center">
<img width="284" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/33ed466c-9a22-4411-bb0b-eb6761cc1157">
</p>
<p align="center">
  Fig 3.
</p>

```v
|calc
         @1
            $aa_sq[7:0] = $aa[3:0] ** 2;
            $bb_sq[7:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[8:0] = $aa_sq + $bb_sq;
         @3
            $cc[4:0] = sqrt($cc_sq);
```

**Retiming**
```v
|calc
         @0
            $aa_sq[7:0] = $aa[3:0] ** 2;
         @1 
            $bb_sq[7:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[8:0] = $aa_sq + $bb_sq;
         @4
            $cc[4:0] = sqrt($cc_sq);
```
<p align="center">
  <img width="332" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3f1d17b0-8ba2-44aa-a4b1-80e2c32e19b3">
</p>
<p align="center">
  Fig 4.
</p>

+ There will be no impact on behavior.

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f4c22366-262d-4241-8dec-c428dc4d974d">
</p>
<p align="center">
  Fig 5. Without pipeline
</p>

<p align="center">
  <img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4a53fc38-ab04-4ea0-a3d5-3e74f20bc601">
</p>
<p align="center">
  Fig 6. With pipeline
</p>

**Identifiers and Types**
+ Type of an identifier determined by symbol prefix and case/delimitation style.
<p align="center">
  <img width="158" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8d4d6c1f-a82a-4ef5-adf8-1b40f7bad737">
</p>
<p align="center">
  Fig 7.
</p>

+ First token must start with two alpha characters.
  - $lower_case : pipe signal
  - $CamelCase : state signal ( Pascal case)
  - $UPPER_CASE : keyword signal
+ Numbers end tokens (after alphas)
  - $base64_value : good
  - $bad_value_5 : bad
+ Numeric identifiers
  - `>>1` : ahead by 1

</details>

<details>
<summary> Labs </summary> 

+ Example
  ```v
  |comp
      
      @1
         $err1 = $bad_input || $illegal_op;
      @3
         $err2 = $err1 || $over_flow;
      @6
         $err3 = $div_by_zero || $err2;
  ```
<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3f3cdbc3-39f3-4cf4-aab8-927b48c39cca">
</p>
<p align="center">
  Fig 8.
</p>

+ Counter and Calculator in pipeline

<p align="center">
  <img width="298" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/96837410-4d83-44f5-86c2-f9ceecfc6568">
</p>
<p align="center">
  Fig 9.
</p>

```v
|calc
      @0
         $reset = *reset;
      @1
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = (>>1$out[31:0]);
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
         $out[31:0] = $reset ? 32'b0 :
                      ($op[1] ? ($op[0] ? $quot : $prod)
                              : ($op[0]? $diff : $sum));
         $cnt[31:0] = $reset ? 0 : (1 + >>1$cnt);
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8e2a534d-fe0d-43a6-97b6-139bc5a41504">
<img width="503" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/1d0f1af7-8ae3-4986-85f1-43b0c19bb772">
</p>
<p align="center">
  Fig 10.
</p>

+ 2-Cycle Calculator
<p align="center">
  <img width="292" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/52da0bab-1d7d-4264-af5a-481c00d26757">
</p>
<p align="center">
  Fig 11.
</p>

```v
|calc 
      @0
         $reset = *reset;
      @1  
         $val1[31:0] = (>>2$out[31:0]);
         $val2[31:0] = $rand2[3:0];
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
         $cnt[0] = $reset ? 0 : (1 + >>1$cnt);
      @2
         $valid[0] = $cnt;
         $rst = ~$valid[0] || $reset;
         $out[31:0] = $rst ? 32'b0 :
                      ($op[1] ? ($op[0] ? $quot : $prod)
                              : ($op[0]? $diff : $sum));
```
<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4b2c78b6-a08b-4195-9bf5-c1ec1799d531">
<img width="476" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/968dc248-1c0c-4d45-a990-32023ff2ab15">
</p>
<p align="center">
  Fig 12.
</p>

</details>

## Validity
<details>
<summary> Introduction </summary> 

+ Validity provides:
  - Easier debug
  - Cleaner design
  - Better error checking
  - Automated clock gating
 
+ Clock gating
  - Clock signals are distributed to every flip flop. CLocks toggle twice per cycle, which consumes power.
  - CLock gating avoids toggling clock signals.
  - TL-verilog can produce fine-grained gating (or enables).
  
</details>

<details>
<summary> Labs </summary>  

+ Distance accumulator

<p align="center">
<img width="341" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/6268ea4f-02f4-44ea-ad0a-00c3bcc10221">
</p>
<p align="center">
  Fig 1.
</p>

```v
|calc
      @1
         $reset = *reset;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] ** 2;
            $bb_sq[31:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
      @4
         $tot_dist[63:0] = 
                   $reset ? '0 :
                   $valid ? >>1$tot_dist + $cc :
                            >>1$tot_dist;
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7c034523-0164-4d80-808c-a59ae8218355">
</p>
<p align="center">
  Fig 2.
</p>

+ 2-Cycle Calculator with Validity

<p align="center">
  <img width="297" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4fafe266-cf7c-4bc9-bf16-c145fcc662b2">
</p>
<p align="center">
  Fig 3.
</p>

```v
|calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[1:0] == 2'b00) ? $sum :
                        ($op[1:0] == 2'b01) ? $diff :
                        ($op[1:0] == 2'b10) ? $prod : $quot;
```

<p align="center">
<img width="956" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/442cb8a9-6c62-4c0b-a27a-f367b3ecff19">
<img width="830" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5eb1d3ca-ca0d-4563-af38-dc2a02bc587f">
</p>
<p align="center">
Fig 4.
</p>

+ Calculator with Single-Value Memory

<p align="center">
  <img width="323" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/81bbd477-b907-40f9-8d03-4582c8c7459f">
</p>
<p align="center">
  Fig 5.
</p>

```v
 |calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $mem[31:0] = $reset ? 32'b0 : 
                         ($op[2:0] == 3'b101) ? $val1 :
                                              >>2$mem;
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[2:0] == 3'b000) ? $sum :
                        ($op[2:0] == 3'b001) ? $diff :
                        ($op[2:0] == 3'b010) ? $prod : 
                        ($op[2:0] == 3'b011) ? $quot : 
                        ($op[2:0] == 3'b100) ? >>2$mem : >>2$out;
```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7d5e4605-d058-45e6-82d1-15f8565c29f2">
<img width="785" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/d2827a11-216d-4e3e-a376-ca69b265b5a1">
</p>
<p align="center">
  Fig 6.
</p>

</details>

<details>
<summary> Hierarchy </summary>

<p align="center">
  <img width="381" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3154b7a2-b8f3-4173-98f3-f06db688fc1e">
</p>
<p align="center">
  Fig 7.
</p>

<p align="center">
  <img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8af0e2ff-58fd-443a-bb89-5c245cf057ff">
</p>
<p align="center">
  Fig 8.
</p>

</details>

# Day-4
## Introduction
<details>
<summary> Micro-architecture of Single Cycle RISC-V CPU </summary>

<p align="center">
  <img width="478" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/bd9a659c-7260-498c-a2bc-55b696c42f92">
</p>

</details>

## Fetch and Decode
<details>
<summary> Implementation Plan </summary> 

<p align="center">
<img width="436" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/641526e6-4ccd-4dd9-ba7a-c61c4aeab0cc">
</p>
<p align="center">
  Fig 1.
</p>

</details>

<details>
<summary> Labs </summary>

+ Navigate to the starter code [starter code](https://myth.makerchip.com/sandbox?code_url=https:%2F%2Fraw.githubusercontent.com%2Fstevehoover%2FRISC-V_MYTH_Workshop%2Fmaster%2Frisc-v_shell.tlv#) 

+ Sample test program to check in viz

```
// External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
```

+ Lab for PC

Program Counter is a register that contains the address of the next instruction to be executed. It is a pointer into the instruction memory, for the instruction that we are going to execute next. Since the memory is byte addressable and each instruction length is 32 bits, the Program Counter adder adds 4 bytes to the address to point to the next address.

For the initial state, before fetching the first ever instruction, there is a presence of a reset signal that will reset the PC value to 0.

For branch instructions, we will have immediate instructions, for which we have to add an offset value to the PC. So for branch instructions, NextPC = Incremented PC + Offset value.

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4bcc36c3-6b4f-475d-8ef9-0970dd2e949c">
</p>
<p align="center">
  Fig 2.
</p>

+ Lab for Instruction Fetch Logic

Here the instruction memory is added to the program. In the Instruction Fetch logic, the instructions are fetched from the instruction memory amd passed to the Decode logic for computation. The instruction memory read address pointer is computed from the program counter and it outputs a 32 bit instruction. (instr[31:0]) . In our case, the Makerchip shell provides us an instantiation to the instruction memory, which contains a test program to compute the sum of numbers from 1 to 9.

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/60641804-d2f2-44dc-91b3-5e48aaea6b56">
  <img width="939" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8dec92ae-607d-4b1a-92e1-dc256d8b61dc">
</p>
<p align="center">
  Fig 3.
</p>

+ Lab for Instruction Decode

In the Instruction Decode logic, all the instructions are decoded for the type of instruction, immediate instructions and the field type instructions. The opcode values are translated into instructions, and all the bit values are interpreted as per defined in the RISC-V ISA.

At first, the Instruction type is decoded using 5 bits of the instruction instr[6:2]. The lower two bits from [1:0] are always equal to '11' for Base integer instructions.
Next we calculate the 32 bit immediate value (imm[31:0]) based on the instruction type.
Other instruction fields like funct7, rs2, rs1, funct3, rd and opcode are extracted from the 32-bit instruction based on the instruction type. We collect all the bit values of funct7, funct3, opcode, rs2, rs1 and rd into a single vector and then decode the type of instruction. At this point valid condtions need to be defined for fields like rs1, rs2, funct3 and funct7 because they are unique to only certain instruction types.

Only 8 operations are implemented at this stage namely BEQ, BNE, BLT, BGE, BLTU, BGEU, ADDI and ADD. The other operations from the RV32I Base Instruction Set will be implemented in the later steps.

<p align="center">
  <img width="515" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3382ad8a-c171-4511-acfc-750e92559fef">
  <img width="465" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/1e7308f0-6ceb-4b9f-ad61-f43fe0893259">
  <img width="457" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4fee566e-2884-4286-bcb6-cf79db7b16f0">
</p>
<p align="center">
  Fig 4.
</p>

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1[4:0] = $instr[19:15];
         $rs2[4:0] = $instr[24:20];
         $rd[4:0] = $instr[11:7];
         $opcode[6:0] = $instr[6:0];
         $funct7[6:0] = $instr[31:25];
         $funct3[2:0] = $instr[14:12];
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c2759d98-9eee-457e-8114-6b7fbf1079a6">
<img width="935" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/a5f607f3-6ff2-4686-90a3-dd12bf03103b">
</p>
<p align="center">
  Fig 5.
</p>

+ Lab for Instruction Decode with Validity

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e3d00438-2e4e-4062-84f7-d35c8211708c">
<img width="911" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8c481ff3-59f0-4aaf-9a83-620a4c9711a9">
</p>
<p align="center">
  Fig 6.
</p>

+ Lab to Decode Individual Instruction

<p align="center">
  <img width="328" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/9ac885b0-78de-4cd0-a46a-3a1c77a378ce">
</p>
<p align="center">
  Fig 7.
</p>

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];         
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/803be52a-1ea9-4070-8ddd-027344e2ca13">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/718c8298-3bba-4f35-846d-d30e820ac344">
</p>
<p align="center">
  Fig 8.
</p>

</details>

## RISC-V Control Logic
<details>
<summary> Labs </summary>

+ Lab for Register File

Most of the instructions are arithmetic instructions or other instructions operating on the source registers. We do regitser file read of these source registers. The register file is provided in the shell to us by the macro instantiation //m4+rf (@1, @1) , which can be viewed under the "NAV-TLV" tab on Makerchip. This macro provides us with a register file that defines the interface signals. The register file of the CPU is capable of performing 2 reads in one cycle, of the source operands, and 1 write per cycle of the desination register.

The two source register fields defined as rs1 and rs2 are fed as inputs to the register file and the outputs are the contents of the source registers. The respective enable bits are set based on the valid conditions for rs1 and rs2 as defined in the previous step. Here, since we are accessing two register files at the same time, hence it is callled as 2-port register file.

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = 1'b0;
         $rf_wr_index[4:0] = 5'b0;
         $rf_wr_data[31:0] = 32'b0;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/d4b25177-6b37-45a0-9fca-3e0ecc1ceec5">
  <img width="955" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/944276ed-22cf-49e8-aa93-8d4a349098cd">
</p>
<p align="center">
  Fig 1.
</p>

+ Lab for ALU Operations (add/addi)

The Arithmetic Logic Unit is the component that computes the result based on the selected operation. The ALU operates on the contents of the two registers coming out of the register file. It performs the respective arithmetic operation on the two registers, and finally the result of the ALU is written back to the memory using the register file write port. At this point, the code only supports ADD and ADDI operations to execute the test code. All operations will be added at a later step.

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = 1'b0;
         $rf_wr_index[4:0] = 5'b0;
         $rf_wr_data[31:0] = 32'b0;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c73d07eb-111c-437e-9218-a6d5df3efcd1">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/77660532-2820-4231-97f3-961023cb4fd5">
</p>
<p align="center">
 Fig 2.
</p>

+ Lab for Register File Write

This step is essential to provide support for instructions that have a destination register (rd) where the output must be stored. The result of the ALU is written back to the memory using the register_file_write port. The register_file_write_enable depends on the validity of the destination register "rd" . The register_file_write_index then takes the value stored in destination register, rd and loads it into the memory in the location as pointed by the register_file_write_index. Since, in RISC-V architecture, x0 register is a hardwired register, whic is always equal to zero, hence it must be made sure that no write operartion is performed on the x0 register. For this, an additional condition to ignore write operation, if the destinaton register is x0 , has been also added.


```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="957" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c0280364-0ab1-4698-b457-4933168d7d41">
<img width="928" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5318b99f-7632-4561-9fec-1ea1ee978181">
</p>
<p align="center">
  Fig 3.
</p>

+ Lab for Branch Instructions

In RISC-V ISA, branches are conditional in nature, which means based on a particular condtion, a specific branch is being taken. Moreover, a branch target pc has to be computed and based on the branch taken value, the pc will choose the new branch target pc when required.

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>1$taken_br ? >>1$br_tgt_pc :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $br_tgt_pc[31:0] = $pc + $imm;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/316acfe9-b9ae-422d-99ae-008a7a7c2336">
<img width="945" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/a807faef-73c9-4572-a555-cc3f9a4364b4">
</p>
<p align="center">
  Fig 4.
</p>

+ Lab for Testbench

 - Now that the implementation is complete, a simple testbench statement can be added to ensure whether the core is working correctly or not. The "passed" and "failed" signals are used to communicate with the Makerchip platform to control the simulation. It tells the platform whther the simulation passed without any errors, failed with a list of errors that can be inferred from the log files, and hence to stop the simulation, if failed.

 - When the following line of code as mentioned below is added on Makerchip, the simulation will pass only if the value stored in r10 = sum of numbers from 1 to 9.
 - Add `*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);`
 - Check log for passed message.

<p align="center">
  <img width="593" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8b740a4b-0dc0-4a65-8f08-e11de4a02eee">
</p>
<p align="center">
  Fig 5.
</p>

</details>

# Day-5
## Pipelining the CPU
<details>
<summary> Introduction to Hazards </summary>

+ Control flow hazard
A control flow hazard, also known as a control hazard or branch hazard, occurs in computer architecture when there is a change in the order of instruction execution due to the outcome of a branch instruction.

+ Read After Write (RAW) Hazard:
  - Occurs when an instruction depends on the result of a previous instruction that has not yet been written to the register file or memory.
  - Example: If Instruction A writes to a register, and Instruction B reads from the same register, and B comes after A in the pipeline, there is a RAW hazard.
 
+ Write After Read (WAR) Hazard:
  - Definition: Occurs when an instruction writes to a register that a previous instruction is still waiting to read.
  - Example: If Instruction A reads from a register, and Instruction B writes to the same register, and B comes before A in the pipeline, there is a WAR hazard.

+ Write After Write (WAW) Hazard:
  - Definition: Occurs when two instructions both write to the same register and the order of the writes is not the same as the order of execution.
  - Example: If Instruction A writes to a register and then Instruction B writes to the same register, and B comes before A in the pipeline, there is a WAW hazard.

<p align="center">
  <img width="509" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/9496c36a-ccff-4bda-be6f-11d7ce4a04d7">
</p>
<p align="center">
  Fig 1.
</p>

+ Solution : Operate it every third cycle.
<p align="center">
  <img width="515" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/66c66115-eef7-451f-8d9d-faab53c6a813">
</p>
<p align="center">
  Fig 2.
</p>

</details>

<details>
<summary> Labs </summary>

+ Lab to create 3-Cycle Valid Signal

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>1$taken_br ? >>1$br_tgt_pc :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $start = >>1$reset && !$reset;
         $valid = $reset ? 1'b0 : $start ? 1'b1 :
                                          >>3$valid;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $br_tgt_pc[31:0] = $pc + $imm;
         *passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8da14f7d-21f4-481a-823e-6d949ed3f779">
  <img width="601" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/17954d20-9ca2-4491-ae1c-4501660ddf7f">
</p>
<p align="center">
  Fig 3.
</p>

+ Taking care of Invalid Cycles

<p align="center">
  <img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7c1f7256-cb61-401f-bad9-a66bce17299f">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/35fe1690-cb0a-4f44-b83a-7fa2335ba62e">
</p>
<p align="center">
  Fig 4.
</p>

+ To modify 3-cycle RISC-V to Distribute Logic

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>3$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $start = >>1$reset && !$reset;
         $valid = $reset ? 1'b0 : $start ? 1'b1 :
                                          >>3$valid;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7be630a6-7a33-4f53-825c-38da0e544f32">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e4557c10-ff02-4e70-89de-446aa607783d">
</p>
<p align="center">
  Fig 5.
</p>

</details>

## Solutions to Pipeline Hazards
<details> 
<summary> Labs </summary>

+ Register File Bypass

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>3$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $start = >>1$reset && !$reset;
         $valid = $reset ? 1'b0 : $start ? 1'b1 :
                                          >>3$valid;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7f472e16-49a6-4e78-be82-d5481edb0ea8">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/991a8b0b-caf2-43a8-95f4-21e1e310e8a0">
</p>
<p align="center">
  Fig 1.
</p>

+ To correct Branch Target Path

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7fe5382a-df36-4c12-9015-7a7521f2a941">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f7e0f4fe-e495-431e-b71a-ee45292efc90">
</p>
<p align="center">
  Fig 2.
</p>

+ Complete Instruction Decode

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/cfd46f35-f662-42c8-9692-8f5fedf77ad2">
  <img width="450" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3b5f98c2-0b48-4eb7-8c81-a5fa81dfe623">
</p>
<p align="center">
  Fig 3.
</p>

+ Complete ALU

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="949" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/352d8b4b-bbf7-4496-b579-4a57aadea9e6">
  <img width="731" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/cdb6b46b-abb3-4f80-ae03-e207bb42cae0">
</p>
<p align="center">
  Fig 4.
</p>

</details>

## Load & Store Instructions and Completing RISC-V CPU
<details>
<summary> Introduction </summary>

<p align="center">
  <img width="490" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/506f0676-de3e-48ab-b153-571a66ed9ef2">
</p>

</details>

<details>
<summary> Labs </summary>

+ Lab to Redirect Loads

```v
 |cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/befdf158-0a6b-46e6-9cb3-8125e6d54ee2">
  <img width="955" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f1eab532-ddb5-4f0a-bcfc-1cb2a842d7d9">
</p>
<p align="center">
  Fig 1.
</p>

+ Lab to Load Data From Memory to Register File

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
      @5
         $ld_data = 'x;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c4bc1d78-e33d-449e-8b26-417d94533df3">
  <img width="477" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/31d88f31-3866-435d-9afa-b0fef320c80a">
</p>
<p align="center">
Fig 2.
</p>

+ Lab to Instantiate Data Memory to CPU

In addition to all of these, we also have a Memory file for which we have load and store instructions. The Store instruction is going to write a value fetched from the register file into the memory. The Load instruction is going to access the memory, take the value from it and them load it into the register file.

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
      /dmem[15:0]
         @4
            $wr = |cpu$dmem_wr_en && (|cpu$dmem_addr == #dmem);
            $value[31:0] = |cpu$reset ? #dmem : $wr ? |cpu$dmem_wr_data :
                                                      $RETAIN;
      @4
         $dmem_wr_data[31:0] = $src2_value;
         $dmem_wr_en = $is_s_instr && $valid;
         $dmem_rd_en = $is_load;
         $dmem_addr[3:0] = $result[5:2];
         ?$dmem_rd_en
            $dmem_rd_data[31:0] = /dmem[$dmem_addr]>>1$value;
      @5
         $ld_data[31:0] = $dmem_rd_data;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/56f33c35-0c61-4e04-ac30-a17050af3389">
<img width="275" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5d0cd0d5-4807-4967-8461-d58b13c9aa1f">
</p>
<p align="center">
  Fig 3.
</p>

+ Add stores and loads to Test program

```
// External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the final result value to byte address 16
   m4_asm(LW, r17, r0, 10000)           // Load the final result value from adress 16 to x17
```

+ Lab for Jump Instructions

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                         >>3$valid_jump && >>3$is_jal ? >>3$br_tgt_pc :
                         >>3$valid_jump && >>3$is_jalr ? >>3$jalr_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $jalr_tgt_pc[31:0] = $src1_value + $imm;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $is_jump = $is_jal || $is_jalr;
         $valid_load = $valid && $is_load;
         $valid_jump = $is_jump && $valid;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load || >>1$valid_jump || >>2$valid_jump);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
      /dmem[15:0]
         @4
            $wr = |cpu$dmem_wr_en && (|cpu$dmem_addr == #dmem);
            $value[31:0] = |cpu$reset ? #dmem : $wr ? |cpu$dmem_wr_data :
                                                      $RETAIN;
      @4
         $dmem_wr_data[31:0] = $src2_value;
         $dmem_wr_en = $is_s_instr && $valid;
         $dmem_rd_en = $is_load;
         $dmem_addr[3:0] = $result[5:2];
         ?$dmem_rd_en
            $dmem_rd_data[31:0] = /dmem[$dmem_addr]>>1$value;
      @5
         $ld_data[31:0] = $dmem_rd_data;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
      m4+cpu_viz(@4)    // For visualisation
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e00536e5-d80d-4b9b-b46b-db86450f4ef6">
  <img width="371" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/32a84296-ab93-485c-a527-69ae5606f57e">
</p>
<p align="center">
  Fig 4.
</p>

</details>

## Wrap up
<details>
<summary> Final RISC-V CPU Core Implementation </summary>

<p align="center">
<img width="958" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/0b67a8e2-7b0d-4590-bf9e-b658a725a558">
  <img width="244" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/b5167c47-af15-4327-a644-3eb62f0dff77">
</p>
<p align="center">
Fig 1.
</p>

The code can be found at https://github.com/Veda1809/RISCV_based_myth/blob/main/final_riscv_core.tlv

+ The code required for the RISC-V Core written in TL-Verilog and System Verilog can be compared by selecting the "Show Verilog" on the makerchip platform under the "E" tab. Upon visualization, a significant code reduction can be seen in the comparision chart.

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/ad025e35-30f6-44c9-ae96-abee7947f4e4">
</p>
<p align="center">
Fig 2.
</p>

</details>
