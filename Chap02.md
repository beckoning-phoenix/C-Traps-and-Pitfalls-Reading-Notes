# Chapter 1 Syntactic Pitfalls

<br/>

## 1. Terminologies

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
   - 
4. The Switch Statement
   
