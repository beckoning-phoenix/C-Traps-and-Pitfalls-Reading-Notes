# Chapter 4 Library Functions

</br>

## 1. Terminologies
   - None

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
   - There must be intervening fseek function between fread and fwrite
   - A wrong program
     ```
     FILE *fp;
     struct record rec;
     while(fread( (char *)&rec, sizeof(rec), 1, fp) == 1){
        /* do something to rec */
        if (/* rec must be rewritten */){
           fseek(fp, -(long)sizeof(rec), 1);
           fwrite( (char *)&rec, sizeof(rec), 1, fp);
        }
     }
     ```
   - A corrected program
     ```
     FILE *fp;
     struct record rec;
     while(fread( (char *)&rec, sizeof(rec), 1, fp) == 1){
        /* do something to rec */
        if (/* rec must be rewritten */){
           fseek(fp, -(long)sizeof(rec), 1);
           fwrite( (char *)&rec, sizeof(rec), 1, fp);
           fseek(fp, 0L, 1);                          \\which is very important to make an interval between fwrite and fread
        }
     }
     ```

3. Buffered output and memory allocation
   - Buffered output function:
     ``` 
     setbuf(stdout, buf);
     ```
     - until buf becomes full or the programmer calls fflush. 
     - BUFSIZ is defined in <stdio. h>
   - A wrong program
     ```
     #include<stdio.h>

     main()
     {
        int c;
        char buf[BUFSIZ];
        setbuf(stdout, buf);
        while((c = getchar()) != EOF) putchar(c);
     }
     //
     ```
     - how to correct it?
       1. ```static char buf[BUFSIZ]```;
       2. moving the delaration of buf outside the main function
       3. allocate the buffer dynamically and never free it
          ```
          char *malloc();
          setbuf(stdout, malloc(BUFSIZ));
          ```
   
4. Using errno for error detection
   - Right way of using errno
     ```
     /* call library function */
     if(error return)
         examine errno;
     ```
   - Whether the library function is called successfully or not, errno may be changed or not changed or equal to 0 or not equal to 0 anyway.

 5. The signal function
    - the only safe thing for a signal handler to do is to set a flag and return, with the assumption that the main pro- gram will test that flag later and discover that a signal has occurred.
   
---

## 3. Key Points in Exercises

   - 5-1. Force output to be unbuffered when debugging to avoid that when a program terminates abnormally, the last few lines of its output are often lost.
     ```
     setbuf(stdout, (char *) 0); \\ as the first statement in the main program.
     ```
   
   - 5-2. Macro version of getchar is in <stdio.h>
   
---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)