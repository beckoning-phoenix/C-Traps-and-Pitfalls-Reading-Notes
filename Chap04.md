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
   - 

---

## 3. Key Points in Exercises


---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)