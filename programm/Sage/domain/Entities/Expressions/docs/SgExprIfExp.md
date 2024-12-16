Представляет собой оператор условного выражения на языке Си ? : .
```cpp
class **SgExprIfExp**: public SgExpression {
  //  (expr1)? expr2 : expr3
  // variant == EXPR_IF
public:
  inline SgExprIfExp(PTR_LLND ll);
  inline SgExprIfExp(SgExpression &exp1;,SgExpression &exp2;, SgExpression &exp3;);
  SgExpression &conditional;();
  SgExpression &trueExp;();
  SgExpression &falseExp;();
  inline void setConditional(SgExpression &c;);
  void setTrueExp(SgExpression &t;);
  void setFalseExp(SgExpression &f;);
  ~SgExprIfExp();
};
```
#### Члены класса

`**SgExprIfExp**`**(PTR_LLND ll)**

document me

`**SgExprIfExp**`**(SgExpression &exp1;,SgExpression &exp2;, SgExpression &exp3;)**

document me

`SgExpression &**conditional**`**()**

document me

`SgExpression &**trueExp**`**()**

document me

`SgExpression &**falseExp**`**()**

document me

`void **setConditional**`**(SgExpression &c;)**

document me

`void **setTrueExp**`**(SgExpression &t;)**

document me

`void **setFalseExp**`**(SgExpression &f;)**

document me






