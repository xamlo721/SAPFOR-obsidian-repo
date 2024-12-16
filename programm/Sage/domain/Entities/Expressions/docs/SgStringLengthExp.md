Представляет выражения длины строки на языке Fortran.
```cpp
class **SgStringLengthExp**: public SgExpression {
  // Fortran index variable bound instantiation
  // variant == LEN_OP
public:
  inline SgStringLengthExp(PTR_LLND ll);
  inline SgStringLengthExp(SgExpression &length;);
  inline ~SgStringLengthExp();
  inline SgExpression *length();
};
```

#### Члены класса

`**SgStringLengthExp**`**(PTR_LLND ll)**

document me

`**SgStringLengthExp**`**(SgExpression &length;)**

document me

`SgExpression ***length**`**()**

document me