Представляет инициализации вида {expr1,expr2,expr3} для всех языков.
```cpp
class **SgInitListExp**: public SgExpression {
  // used for initializations.  form: { expr1,expr2,expr3}
  // variant == INIT_LIST
public:
  inline SgInitListExp(PTR_LLND ll);
  inline SgInitListExp(SgExpression &expr;_list);
  inline SgInitListExp(int n, SgExpression *components);
  inline ~SgInitListExp();
  
  inline SgExpression *arg(int i); // the i-th term
  int numberOfArgs();
  inline void setArg(int i, SgExpression &e;);
};
```

#### Члены класса
`**SgInitListExp**`**(PTR_LLND ll)**

document me

`**SgInitListExp**`**(SgExpression &expr;_list)**

document me

`**SgInitListExp**`**(int n, SgExpression *components)**

document me

`SgExpression ***arg**`**(int i)**

document me

`int **numberOfArgs**`**()**

document me

`void **setArg**`**(int i, SgExpression &e;)**



