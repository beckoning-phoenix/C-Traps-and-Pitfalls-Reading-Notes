# Chapter 4 Linkage

</br>

## 1. Terminologies

   - external object
     - A declaration appearing outside of any function body

---

## 2. Key Points about Linkage

1. What is a linker?
   - A typical linker combines several object modules produced by a compiler or assembler together into a single entity, sometimes called a load module or an executable file, that the operating system can execute directly.
   - The most important thing about linkage in writing C programme: Avoid Name Conflicts!!

2. Declarations vs definitions
   - Three types of declaration
     ```
     int a;        // only definition
     int a = 7;    // definition and memory allocation
     extern int a; // a reference to an external object but not definition
     ```
     A program that includes 
     ```
     extern int a 
     ```
     must say 
     ``` 
     int a 
     ```
     somewhere else, either in the same program file or a different one.

3. Name conflicts and the static modifier
   - Name conflicts
     - Two external objects with the same name are the same objects.
     - Duplicating external objects either represents a error or shares a single instance
   - Static modifier
     - A declaration modified by the static modifier is hidden from other files.
    
4. Arguments, parameters, and return values
   - (Omitted, as it's now hard to see the programs compiled by the pre-ANSI C compiler)

5. Checking external types
   - As the subtitle said, make sure that the external types are the same, expecially be careful about the char arrays and char pointers, they are NOT the same!!

6. Header files
   - Expanding the include statement
     ```
     //in "file.h"
     extern char filename[];
     ```
     ```
     //in "file.c"
     #include "file.h"
     char filename[] = "etc/passwd";
     ```
     Write references to variables in .h file and declare/define it in .c file 
---

## 3. Key Points in Exercises

   - 4-1. a program to judge whether the machine is litt-endian or big-endian:
        ```
        extern short n;
        ```
        and in another file:
        ```
        long n;
        n = 37;
        ```
        if n (short type) is 37, then it should be little-endian; if n is 0, then it should be big-endian.

   - 4-2. Some C implementations have two versions of printf, one of which implements the floating-point format items %e, %f, and %g and the other of which does not.
     In some systems, the programmer must explicitly tell the linker whether floating-point arithmetic is being used. Others try to decide automatically by having the compiler tell the linker if it sees any floating-point operations in the program.
---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)