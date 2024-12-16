Представляет векторные константы Fortran вида \[expr1,expr2,expr3\].

```cpp
class **SgVecConstExp**: public SgExpression {
  // a vector constant of the form: [ expr1, expr2, expr3]
  // variant == VECTOR_CONST
public:
  inline SgVecConstExp(PTR_LLND ll);
  inline SgVecConstExp(SgExpression &expr;_list);
  inline SgVecConstExp(int n, SgExpression *components);
  inline ~SgVecConstExp();
  
  inline SgExpression *arg(int i); // the i-th term
  inline int numberOfArgs();
  inline void setArg(int i, SgExpression &e;);
};
```

#### Члены класса

`**SgVecConstExp**`**(PTR_LLND ll)**

document me

`**SgVecConstExp**`**(SgExpression &expr;_list)**

document me

`**SgVecConstExp**`**(int n, SgExpression *components)**

document me

`SgExpression ***arg**`**(int i)**

document me

`int **numberOfArgs**`**()**

document me

`void **setArg**`**(int i, SgExpression &e;)**

document me


