Представляет собой разыменования указателей на языке Си.

```cpp
class **SgPointerDerefExp**: public SgExpression {
  // pointer dereferencing
  // variant == DEREF_OP
public:
  inline SgPointerDerefExp(PTR_LLND ll);
  inline SgPointerDerefExp(SgExpression &pointerExp;);
  inline ~SgPointerDerefExp();
  inline SgExpression *pointerExp();
};
```


#### Члены класса
`**SgPointerDerefExp**`**(PTR_LLND ll)**

document me

`**SgPointerDerefExp**`**(SgExpression &pointerExp;)**

document me

`SgExpression ***pointerExp**`**()**

document me
