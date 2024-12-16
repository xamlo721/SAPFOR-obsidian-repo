Представляет ссылки на массивы для всех языков.

```cpp
Represents array references, for all languages.

class  **SgArrayRefExp**: public SgExpression {
  // an array reference
  // variant == ARRAY_REF
public:
  inline SgArrayRefExp(PTR_LLND ll);
  inline SgArrayRefExp(SgSymbol &s;);
  inline SgArrayRefExp(SgSymbol &s;, SgExpression &subscripts;);
  inline SgArrayRefExp(SgSymbol &s;, SgExpression &sub1;,SgExpression &sub2;);
  
  inline SgArrayRefExp(SgSymbol &s;, SgExpression &sub1;,SgExpression &sub2;,
                       SgExpression &sub3;);  
  inline SgArrayRefExp(SgSymbol &s;, SgExpression &sub1;,SgExpression &sub2;,
                       SgExpression &sub3;,SgExpression &sub4;);
  inline ~SgArrayRefExp();
  inline int numberOfSubscripts();  // the number of subscripts in reference
  inline SgExpression *subscripts();
  inline SgExpression *subscript(int i);
  inline void addSubscript(SgExpression &e;);
  inline void setSymbol(SgSymbol &s;);
};
```
#### Члены класса
`**SgArrayRefExp**`**(PTR_LLND ll)**

document me

`**SgArrayRefExp**`**(SgSymbol &s;)**

document me

`**SgArrayRefExp**`**(SgSymbol &s;, SgExpression &subscripts;)**

document me

`**SgArrayRefExp**`**(SgSymbol &s;, SgExpression &sub1;,SgExpression &sub2;)**

document me

`**SgArrayRefExp**`**(SgSymbol &s;, SgExpression &sub1;,SgExpression &sub2;,SgExpression &sub3;)**

document me

`**SgArrayRefExp**`**(SgSymbol &s;, SgExpression &sub1;,SgExpression &sub2;,SgExpression &sub3;,SgExpression &sub4;)**

document me

`int **numberOfSubscripts**`**()**

document me

`SgExpression ***subscripts**`**()**

document me

`SgExpression ***subscript**`**(int i)**

document me

`void **addSubscript**`**(SgExpression &e;)**

document me

`void **setSymbol**`**(SgSymbol &s;)**

document me

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[18 Instrument - isReferenceToCollection]]
[[1 Expand Syntax - isReferenceToElementField]]
