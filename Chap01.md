# Chapter 1 Lexical Pitfalls

<br/>

## 1. Terminologies

- token
  - a part of a program that plays much the same role as a word in a sentence: 

- lexical analyzer
  - the part of a compiler that breaks a program up into tokens 

---

## 2. Key Points about Lexical Pitfalls

1. = is not ==

2. & and | are not && and ||

3. Greedy (Maximal Munch) Lexical Analysis Strategy
   - "repeatedly bite off the biggest possible piece"
   - ```a---b``` means ```a-- -b``` 
   - ```y = x/*p``` , ```y = x / *p``` , ```y = x / (*p)``` mean:

     ```y = x(/*)p``` , ```y = x / (*p)``` , ``` y = x / (*p) ``` 
4. Integer Constants
   - 010 (octal, 010 means 8) <---> 10 (decimal)
5. Strings and Characters
   - single quote ('a') is just another way of an integer (0141 or 97)
   - double quote ("a") is a character array (['a', '\0'])
   - ```printf("\n") ``` BUT NOT ```printf('\n')```!!!)
   - 'yes' <---> "yes" (Ps. In gcc v2.95 and Visual C++ 6.0, 'yes' == 's'(the value of the last character))

---

## 3. Key Points in Exercises 

- 1-1. A program that can judge whether the compliler supports nested comment or not
    ```
    /*/**/0*/**/1
    /* /* */ 0 */ * */ 1   // 1, if support nested comment
    /* /* */ 0 * /* */ 1   // 0*1==0, if not support nested comment
    ```

- 1-2. When using C or writing a C compiler, AVOID using nested comment.

- 1-3. A review of the greedy lexical analysis stratege

- 1-4. Answer: a++ + ++b  
  - Question: According to greedy strateg,why not a++ ++ +b?
  - Answer: Because a++ is not an lvalue, can't be an operand of ++

---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)
