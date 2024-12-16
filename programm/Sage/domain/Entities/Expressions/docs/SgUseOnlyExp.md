Представляет собой ONLY атрибут инструкций USE для Fortran 90.

```cpp
class **SgUseOnlyExp**: public SgExpression {
  // Fortran 90 USE statement ONLY attribute 
  // variant == ONLY_NODE
public:
  inline SgUseOnlyExp(PTR_LLND ll);
  inline SgUseOnlyExp(SgExpression &onlyList;);
  inline ~SgUseOnlyExp();
  inline SgExpression *onlyList();
};
```

#### Члены класса

`**SgUseOnlyExp**`**(PTR_LLND ll)**

document me

`**SgUseOnlyExp**`**(SgExpression &onlyList;)**

document me

`SgExpression ***onlyList**`**()**

document me
