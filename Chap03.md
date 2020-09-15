# Chapter 3 Semantic Pitfalls

</br>

## 1. Terminologies 

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
          printf(q-p) \\ which means i 
          ```
        - If p and q don't point to the  elements of an array, there is no way to guarantee q-p is i even that the distance between p and q is an integral multiple of an array element!
   - a, *a, &a
     - a: the address of element 0 of a except the sizeof operand(the size of the whole array instead of only one element)
     - *a: 
     - &a: In most earlier versions of C, there is no notion of the address of an array - &a is either illegal or equivalent to a.
   -  
2. Pointers that are not arrays

3. Array declarations as parameters 

4. Eschew synecdoche

5. Null pointers are not null strings

6. Counting and asymmetric bounds

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
