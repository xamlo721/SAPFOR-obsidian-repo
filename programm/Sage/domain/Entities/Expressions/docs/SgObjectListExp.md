Представляет эквивалентность в Фортране, список имен и общие инструкции.

```cpp
class **SgObjectListExp**: public SgExpression {
  // used for EQUIVALENCE, NAMELIST and COMMON statements
  // variant == EQUI_LIST, NAMELIST_LIST, COMM_LIST
public:
  inline SgObjectListExp(PTR_LLND ll);
  inline SgObjectListExp(int variant, SgSymbol &object;, SgExpression &list;);
  inline SgObjectListExp(int variant,SgExpression &objectRef;, SgExpression &list;);
  inline ~SgObjectListExp();
  inline SgSymbol *object();
  inline SgExpression *objectRef();
  inline int listLength();
  inline SgSymbol *symbol(int i);        //i'th symbol
  inline SgExpression *objectRef(int i);  //i'th symbol
};
```

#### Члены класса

`**SgObjectListExp**`**(PTR_LLND ll)**

document me

`**SgObjectListExp**`**(int variant, SgSymbol &object;, SgExpression &list;)**

document me

`**SgObjectListExp**`**(int variant,SgExpression &objectRef;, SgExpression &list;)**

document me

`SgSymbol ***object**`**()**

document me

`SgExpression ***objectRef**`**()**

document me

`int **listLength**`**()**

document me

`SgSymbol ***symbol**`**(int i)**

document me

`SgExpression ***objectRef**`**(int i)**

document me
