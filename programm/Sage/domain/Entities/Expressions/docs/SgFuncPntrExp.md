Представляет использование в языке Си указателей на функции.

```cpp
class **SgFuncPntrExp**: public SgExpression {
  // (functionpointer)(expr1,expr2,expr3)
  // variant == FUNCTION_OP
public:
  inline SgFuncPntrExp(PTR_LLND ll);
  inline SgFuncPntrExp(SgExpression &ptr;);
  inline ~SgFuncPntrExp();
  inline SgExpression *funExp();
  inline void setFunExp(SgExpression &s;);
  inline int numberOfArgs();
  inline SgExpression *arg(int i);
  inline void addArg(SgExpression &arg;);  // add an argument.
  SgExpression* AddArg(SgSymbol *thefunc, char *name, SgType &); 
              // add a formal parameter
              // to a pointer to a function prototype or parameter.
              // this returns the expression
};
```
#### Члены класса
`**SgFuncPntrExp**`**(PTR_LLND ll)**

document me

`**SgFuncPntrExp**`**(SgExpression &ptr;)**

document me

`SgExpression ***funExp**`**()**

document me

`void **setFunExp**`**(SgExpression &s;)**

document me

`int **numberOfArgs**`**()**

document me

`SgExpression ***arg**`**(int i)**

document me

`void **addArg**`**(SgExpression &arg;)**

document me

`SgExpression **AddArg**`**(SgSymbol *thefunc, char *name, SgType &)**

Этот метод можно использовать для добавления формального параметра к указателю на прототип или параметр функции. Этот метод возвращает это выражение. Подробное описание этого метода приведено в разделе Указатели на функции.



