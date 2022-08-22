# Memory
It is very important to understand what memory is, and how to handle it
One of the biggest metrics of how good a software is, is how much memory it uses. the less memory a software uses, the better it is. 
> This is coupled with [[space complexity]] notion

Low memory allocation is usually managed by the operating system, with some optimization available from the compilers. but calls to allocate the memory are done by the program. depending on the programming language used, memory management could be easier or harder. but in all cases, it's important to understand how memory management works to be able to fully use the programming language to its limit.

>**NOTE:** modern CPUs operate on either a 32bit or 64bit addressing system, so in theory, the smallest allocated memory slot is 32bit, but usually compilers use optimizations to get around this limitation

It could be helpful to check the [[Hardware Layer]] to better understand how it works, specially the [[Endiannes]], but for now, it's important to understand, that in the lowest form, ALL DATA are stored as Bits, these Bits are collected into Bytes from which we derive all the other data types.