# Chapter 4 Library Functions

</br>

## 1. Terminologies
   - 

---

## 2. Key Points about Library Functions

1. getchar returns an integer
   - A wrong program to read from standard input (Very Common!)
     ```
     #include<stdio.h>

     int main()
     {
        char c;

        while((c = getchar())!= EOF)
            putchar(c);
     }
     ```
     c is declared as char type instead of int, which means that it is impossible for c to hold every possible character as well as EOF.

2. Updating a sequential file
   
---

## 3. Key Points in Exercises


---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)