Представляет экземпляры, связанные с индексной переменной Fortran.

```cpp
class **SgImplicitTypeExp**: public SgExpression {
  // Fortran index variable bound instantiation
  // variant == IMPL_TYPE
public:
  inline SgImplicitTypeExp(PTR_LLND ll);
  inline SgImplicitTypeExp(SgType &type;, SgExpression &rangeList;);
  inline ~SgImplicitTypeExp();
  inline SgType *type();
  inline SgExpression *rangeList();
  inline char *alphabeticRange();
};
```
#### Члены класса

`**SgImplicitTypeExp**`**(PTR_LLND ll)**

document me

`**SgImplicitTypeExp**`**(SgType &type;, SgExpression &rangeList;)**

document me

`SgType ***type**`**()**

document me

`SgExpression ***rangeList**`**()**

document me

`char ***alphabeticRange**`**()**

document me