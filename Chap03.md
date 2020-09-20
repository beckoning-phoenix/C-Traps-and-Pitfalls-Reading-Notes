# Chapter 3 Semantic Pitfalls

</br>

## 1. Terminologies 

   - synecdoche
     - a more comprehensive term is used for less comprehensive or vice versa; as whole for part or part for whole, genus for species or species for genus, etc.
---

## 2. Key Points about Semantic Pitfalls

1. Pointers and arrays
   - Two things  stand out about C arrays
      1. C has only one-dimensional arrays, and an element of an array may be an object of any type
      2. Only two things can be done to an array: determine its size and obtain a pointer to element 0 of the array 

   - Adding an integer to a pointer is generally DIFFERENT from adding that integer to the bit representation of that pointer!!!
     
     If ip points to an integer, ip+1 points to the next integer in the machine's memory, which, for most modern computers, is not the next memory location.
        - ```
          int *q =p + i;
          printf(q - p); // which means i 
          ```
        - If p and q don't point to the  elements of an array, there is no way to guarantee q-p is i even that the distance between p and q is an integral multiple of an array element!
   - a, *a, &a
     - a: the address of element 0 of a except the sizeof operand(the size of the whole array instead of only one element)
     - *a:  a reference to element 0 of a, as *(a+i) is equivalent to a[i] , i[a] and *(i+a)
     - &a: In most earlier versions of C, there is no notion of the address of an array - &a is either illegal or equivalent to a.
   - Two-dimensional arrays
     - the pointer to an array
       ```
       int calendar[12][31]; 
       int (*monthp)[31];    // the pointer to an array
       monthp = calendar;
       ```
     - the relationship between pointers and arrays(summary):
       ```
       int (*monthp)[31];
       for(monthp = calendar; monthp < &calendar[12]; monthp++){
           int *dayp;
           for(dayp = *monthp; dayp < &(*month)[31]; dayp++)
                *dayp = 0;
       }
       ```

2. Four examples in using char arrays 
   1. ```
      char *r;    // wrong, because the memory of r is not allocated 
      strcpy(r, s);
      strcat(r, t);
      ```
   2. ```
      char r[100]; // right, allocating memory for r, but the memory should be constant and may be not big enough. 
      strcpy(r, s); 
      strcat(r, t);
      ```
   3. ```
      char *r, *malloc();
      r = malloc(strlen(s) + strlen(t));
      strcpy(r, s);
      strcat(r, t);
      // wrong ,because:
      //(1) malloc may fail, returning a null pointer
      //(2) allocates memory explicitly and must therefore free it explicitly
      //(3) r requires memory of n+1 characters instead of n;
      ```
   4. ```
      char *r, *malloc();
      r = malloc(strlen(s) + strlen(t) + 1);
      if(!r) {
          complain();
          exit();
      }
      strcpy(r, s);
      strcat(r, t);

      /* some time later */
      free(r);
      // right
      ```

3. Array declarations as parameters 
   1. In some occasions, C will automatically converts an array declaration to the corresponding pointer decalaration
      ```
      int strlen(char s[]){}
      int strlen(char *s){}  // totally the same
   
      printf("%s\n, hello");
      printf("%s\n, &hello[0]"); // totally the same
   
      main(int argc, int *argv[])
      main(int argc, int **argv)  // totally the same
      ```
   2. But in other occasions, C will not automatically do such convertion:
      ```
      extern char *hello;
      extern char hello[];
      ```

4. Eschew synecdoche
   - Copying a pointer does not copy the thing it adresses. 
     char *p, *q;
     p = "xyz";
     q = p;
     q[1] = 'Y';
     printf(p); //xYz, p and q actually point to the same memory.   
     ```

5. Null pointers are not null strings
   - Don't ask what is in the memory the null pointer addresses
     ```
     if (p == (char *) 0) ... //valid
     if (strcmp(p, (char *) 0) == 0) //not valid
     ```

6. Counting and asymmetric bounds
   - Off-by-one error (avoid such error by using asymmetric bounds)
     ```
     int a[10], i;
     for (int i = 0; i < 10; i++) a[i] = 0; \\ instead of i <= 9
     ```
   - Using asymmetric bounds in dealing with buffers of various sorts
     ```
     #define N 1024
     static char buffer[N];
     static char *bufptr;
     *bufptr++ = c;       //put a character c into the buffer
     bufptr = &buffer[0]; //initially say the buffer is empty
     bufptr = buffer;     //initially say the buffer is empty
     ``` 
   - Using asymmetric bounds to write out a buffer-load
     ```
     void
     bufwrite(char *p, int n)
     {
        while(--n >= 0)
        {
           if(bufptr == &buffer[N]) flushbuffer(); 
           /*
           the address of the nonexistent element just past the end of an array may be taken and used for assignment and comparison purposes. But it is illegal actually to refer to that element!
           */

           *bufptr++ = *p++;
        }
     }
     ``` 
   - Using memcpy function to accelerate the buffer-load function
     ```
     void 
     bufwrite(char *p, int n)
     {
        while(n > 0)
        {
           if(bufptr == &buffer[N]) flushbuffer();
           int k, rem;
           rem = N - (bufptr - buffer);
           k = n > rem? rem: n;
           memcpy(bufptr, p ,k);
           bufptr += k;
           p += k;
           n -= k;
        }
     }
     ```

7. Order of evaluation
   - The order of evaluation of the operand
     - &&, ||   : lvalue first
     - a < b    : a or b frist or even parallel
     - g(x, y)  : x or y first or even parallel
     - g((x,y)) : x first and discarded and then y
   - An incorrect instance
     ```
     i = 0;
     while(i < n)
     {
        y[i] = x[i++];
        \*
        *There is no guarantee that the address of y[i] will be evaluated before i is incremented. On some implementations, it will; but on others, it won't.
        *\
     }
     ```

8. The &&, || and ! operators
   - The difference between && and & (also, || and |)

9. Integer Overflow
   - Two ways of avoiding integer overflow
     1. ```
        if((unsigned)a + (unsigned)b > INT_MAX) complain(); \\INT_MAX is defined in <limits.h> in ANSI C standard.
        ```
     2. ```
        if(a > INT_MAX - b) complain(); \\recommended
        ```

10. Returning a value from main
    - Like any onther function, main is presumed to yield an int value if no other return type is declared for it.
    - 0 return indicates success and any other value indicates failure

---

## 3. Key Points in Exercises

- 3-1. A bufwrite function breaking the asymmetric bounds rule.

- 3-2. (omitted)

- 3-3. Binary search algorithm using assymetric bounds rule
  ```
  int * bsearch(int *t, int n, int x){
     int l = 0; r = n;
     while （l < r)
     {
        int mid = (l + r) / 2;
        if (x < t[mid]) r = mid;
        else if (x > t[mid]) l = mid + 1;
        else return t + mid;
     }
     return NULL;
  }
  ```

---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)
