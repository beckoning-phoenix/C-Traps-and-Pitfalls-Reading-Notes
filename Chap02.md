# Chapter 1 Syntactic Pitfalls

<br/>

## 1. Terminologies

   - Operator precedence table (operators near the top bind most tightly)

     | operators                          | associativity |
     |:-----------------------------------|:--------------|
     | () [] -> .                         | left          |
     | ! ~ ++ -- - (type) * & sizeof      | right         |
     | * / %                              | left          |
     | + -                                | left          |
     | << >>                              | left          |
     | < <= > >=                          | left          |
     | == !=                              | left          |
     | &                                  | left          |
     | ^                                  | left          |
     | \|                                 | left          |
     | &&                                 | left          |
     | \|\|                               | left          |
     | ?:                                 | right         |
     | assignments                        | right         |
     | ,                                  | left          |

---

## 2. Key Points about Syntactic Pitfalls

1. Understanding Function Declarations
   - ```(*(void(*)())0)(); //a subroutine whose address was stored in location zero.```
   - ```fp() is just an abbreviation of (*fp)()  \\ANSI C standard```

2. Operation Precedence
   - ``` if (flags & FLAG != 0)  \\ if (flags & (FLAG != 0)), != bind more tightlt than &```
   - ```r = hi <<4 + low & 7  \\ r = （hi<< (4 + low)） & 7, + bind more tightlt than <<， << bind more tightly than &```
   - ```*p()  \\ * (p()), () bind more tightly than *```
   - ```*p++  \\ * (p++), ++ bind more tightly than *```
   - ```while(c = getc(in) != EOF)  \\while(c = (getc(in) != EOF)), comparison operator bind more tightly than assignments)```

3. Watch the Semicolons
   - After an if or while clause
   - At the end of a declaration just before a function definition

4. The Switch Statement
   - Bug or feature? be careful of leaving out a break statement

5. Calling functions
   - Unlike some other programming languages, C requires a function call to have an argument list even if there are no arguments. 

6. The dangling else problem
   - ```
     if (x == 0)
             if (y == 0) error(); 
     else {
             z = x + y; 
             f(&z);
     }

     // the way the former program execute actually

     if (x == 0) {
             if (y == 0) error();
     } 
     else {
             z = x + y; 
             f(&z);
     }
     ```

---

## 3. Key Points in Exercises 

- 2-1. The aim of permitting an extra comma in an initializer list in C is to make it more convenient for the using of automatic tools like editors.

- 2-2. Other ways of separating statements in other languages(like Fortran, Snobol, Shell, Awk, Ratfor,...) (P.s. In fact, it has nothing to do with the KEY Point of this book, just read it for fun :-) )

---

Thanks a lot for reading!

[My Github Page](https://github.com/beckoning-phoenix)