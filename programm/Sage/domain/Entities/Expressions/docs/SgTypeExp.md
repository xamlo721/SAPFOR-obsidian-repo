Представляет выражения типа Fortran.
```cpp
class **SgTypeExp**: public SgExpression {
  // Fortran type expression 
  // variant == TYPE_OP
public:
  inline SgTypeExp(PTR_LLND ll);
  inline SgTypeExp(SgType &type;);
  inline ~SgTypeExp();
  inline SgType *type();
};
```

#### Члены класса

`**SgTypeExp**`**(PTR_LLND ll)**

document me

`**SgTypeExp**`**(SgType &type;)**

document me

`SgType ***type**`**()**

document me