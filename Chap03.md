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
   - 

7. Order of evaluation

8. The &&, || and ! operators

9. Integer Overflow

10. Returning a value from main

---

## 3. Key Points in Exercises

- 3-1.

- 3-2.

- 3-3.

---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)
