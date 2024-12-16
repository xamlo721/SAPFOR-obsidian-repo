Представляет выражения Fortran seq.
```cpp
class **SgSeqExp**: public SgExpression {
  // Fortran index variable bound instantiation
  // variant == SEQ
public:
  inline SgSeqExp(PTR_LLND ll);
  inline SgSeqExp(SgExpression &exp1;, SgExpression &exp2;);
  inline ~SgSeqExp();
  inline SgExpression *front();
  inline SgExpression *rear();
};
```

#### Члены класса

`**SgSeqExp**`**(PTR_LLND ll)**

document me

`**SgSeqExp**`**(SgExpression &exp1;, SgExpression &exp2;)**

document me

`SgExpression ***front**`**()**

document me

`SgExpression ***rear**`**()**

document me