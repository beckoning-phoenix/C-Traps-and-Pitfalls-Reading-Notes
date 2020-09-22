# Chapter 6 The Preprocessor

</br>

## 1. Terminologies

   - None

---

## 2. Key Points about Preprocessor

1. Spaces matter in macro definitions
   - ```#define f (x) ((x)-1)``` means f represents ```(x) ((x)-1)```
      
2. Macros are not functions
   - Right macro definitions
     ```
     #define abs(x) (((x)>=0)?(x):-(x))
     ```
     - a wrong example
       ```
       #define abs(x) x>0?x:-x 
       ```
       - which abs(a-b) will expand into a-b>0?a-b:-a-b
   - The arguments may be something like z++, which causing error
     - max macro
     - putc macro
       ```
       #define putc(x,p) (--(p)->_cnt>=0?(*(p)->_ptr++=(x)):_flsbuf(x,p))
       ```
     - toupper macro
       ```
       #define toupper(c) ((c)>='a' && (c)<='z'?(c)+('A'-'a'):(c))
       ```
   - The macro may expand too large

  3. Macros are not statements
     - Wrong example of define assert macro
       - 1st wrong version
         ```
         #define assert(e) if (!e) assert_error(__FILE__,__LINE__) //wrong

         if(x > 0 && y > 0)
             assert(x > y); // structure error: else
         else 
             assert(y > x); 
         ```
       - 2nd wrong version
         ```
         #define assert(e) {if (!e) assert_error(__FILE__,__LINE__) }//wrong

         if(x > 0 && y > 0)
             assert(x > y); //syntax error: extra ';'
         else 
             assert(y > x); 
         ```
       - the right definition
         #define assert(e) ((void)((e)||_assert_error(__FILE__,__LINE__)))
  4. Macros are not type definitions
     - Differences between type definitions using typedef and using macros
       ```
       #define T1 struct foo *
       typedef struct foo *T2;
       T1 a, b; // b is a struct
       T2 a, b; // b is a pointer to the struct
       ``` 

---

## 3. Key Points in Exercises

   - 6-1. ```
          static int max_temp1, max_temp2;
          #define max(a,b) (max_temp1=(a) ,max_temp2=(q) ,max_temp1>max_temp2?max_temp1:max_temp2)
          ```
   - 6-2. (omitted, useless)
   
---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)