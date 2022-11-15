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

