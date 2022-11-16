# Reverse engineering

Video source: [pwn.college 2021 - module 7 - reverse engineering](https://yewtu.be/playlist?list=PL-ymxv0nOtqrGVyPIpJeostmi7zW5JS5l)

#### Introduction:

What is reverse engineering:

"Forward engineering": the creation of a program

* 1. Figure out what you want to write
* 2. Code it
* 3. Compile it (can include JIT)
* 4. Run it

At every point in this process information is lost. Reverse engineering is the proccess of getting this information back.

Lost in design: what was the meaning of this code and who the hell wrote this (code is not self explainatory)

Lost in compilation and assembly process:

* Comments (is not needed for the function of the program)
* Variables names (become memory locations)
* Function names
* Structure (classes, structs, etc) data.
* Sometimes, entire algorithms (optimization)!

We also lost type information. For example that something is a char array in c.

How do we get it back (from the compiled code)?:

(Maybe needed the have more know how on assembly)

Forward engineering tools:

* Vim/ and IDE
* GCC
* strings
* strip

What is the reverse engineering process:  
Every step in the reverse engineering process is imperfect and relies on some amount of human help  
Typically, a reverser use several reverse engineering tools to build up a mental model of the target software.  
This art is the focus of this module: how do we reverse engineer the design *from a binary*?

* Disassable it
* Decompile it
* Lots of thinking (can be both manually or automatically, using intuition to find out the original intent of the source code. This is a art, putting your mind in the shoes of the developer and trying to understand the original intent of the developer and his/hers source code).
* Understanding the actual output of the reverser  
Again: *_This is not easy to do, and you need to actually understand how this works before you can make any use of this technique_*

#### Functions and frames:

A **program** consist of:

* **modules**..
* that are made up of **functions**..
* that contain **blocks**..
* of **instructions**..
* that operate on **variables** and **data structures**

Functions:  
Functions represent fairly well-encapsulated functionality:  
Most functions have well-defined goals, such as:

* Get some data
* Calculate/retrieve/validate data
* Dispatch other functions
* Perform some action on the outside world (via system calls)

Initially, functions can be reversed-engineered 	in isolation. Later you can get an understanding of how they fit together.

Functions: the control graph:  
Functions are represented as a **graph**  
Each **block** is a set of instructions that will execute one after the other.  
Blocks are joined by **edges**, representing conditional and unconditional jumps.  
By understanding what the blocks do and what conditions trigger what edges, you can understand the funcntion's logic!  
Functions often begin with a **prologue** and end with an **epilogue**.  
The prologue set ups the stack frame, with the epilogue tears this down.

What is the stack:  
"The stack is a memory location". The stack is a region of memory used to store local variables and call context.  
The stack grows backwards.  
When you **push** the stack, **rsp** is reduced by 8.	
When you **pop** the stack, **rsp** in _increased_ by 8.  
The stack is conceptualized vertically or horizontally. (Grows up or down, or left to right, remember the lessons here: this depends from person to person.)


#### Data access:
Reminder: data can be in:  
**.data** used for pre-initialized global writable data (such as global arrays with initial values)  
**.rodata** used for global read-only data (such as string constants)  
**.bss** used for uninitialized global writable data (such as global arrays without initial values)  
**stack** used for statically-allocated local variables   
**heap** used for dynamically-allocated (**malloc()**ed) variables.


#### Static tools:
*Static* (as opposed to dynamic) reverse engineering tools: analyzing the program at rest.  
What is in the elf file, not what the file does to get it's work done.  
Some examples are: katai struct, nm, strings, objdump, checksec. (These are the simple tools).  
More advanced tools are:  
Advanced dissasamblers (these tools are all static, but some do support dynamic features).

These cover some understanding about how the program was written, why that program was written and what the program's logic is.

* Commercial:
	* IDA (Interactive DissAssembler) pro: the gold standard of dissasamblers [link](https://hex-rays.com/ida-pro/) (insanely expensive)
	* Binary Ninja: IDA's main competitor [link](https://binary.ninja) (also expensive, free version see below)

* Free:
	* Binary Ninja cloud: a version of Binary Ninja that runs in your browser. [link](https://cloud.binary.ninja) (no setup cost, nice and easy to use)

* Open Source:
	* Angr management: an academic binary analasis framework [link](https://github.com/angr/angr-management) 
	* Ghidra: a reversing tool created by the NSA [link](https://ghidra-sre.org/) (use in class, it also is in the main Kali Linux and Parrot OS repos)
	* Cutter: a reversing tool created by the radare2 open source project [link](https://cutter.re)

**THERE IS NO SHORTAGE OF GOOD TOOLS THAT FITS YOU NEEDS!**

#### Dynamic tools:
Dynamic (as opposed to static) reverse engineering is the process of analyzing the program at runtime.  
Simpel tools:  
**Itrace** traces libary calls  
**Strace** traces system calls  
Running the program with multiple different inputs might get you further:

* Itrace the program with input A
* Itrace the program with input B
* See if you can reverse the algorithm from looking at the input and output
* Still does not scale to complex algorithms

Left off here on 16th of november 2022.

#### Real world applications:
