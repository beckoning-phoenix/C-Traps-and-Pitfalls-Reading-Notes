# Chapter 1 Syntactic Pitfalls

<br/>

## 1. Terminologies

## 2. Key Points about Syntactic Pitfalls

1. Understanding Function Declarations
   - ```(*(void(*)())0)(); //a subroutine whose address was stored in location zero.```

2. Operation Precedence
   - ``` if (flags & FLAG != 0)  \\ if (flags & (FLAG != 0)), != bind more tightlt than &```
   - ```r = hi <<4 + low  \\ r = hi<< (4 + low), + bind more tightlt than <<```
   - ```*p()  \\ * (p()), () bind more tightly than *```
   - ```*p++  \\ * (p++), ++ bind more tightly than *```
   
