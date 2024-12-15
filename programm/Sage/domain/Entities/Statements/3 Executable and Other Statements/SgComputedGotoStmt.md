Представляет собой вычисленную  инструкцию goto на Fortran.

```cpp
class **SgComputedGotoStmt**: public SgLabelListStmt {
  // the fortran goto
  // variant == COMGOTO_NODE
public:
  inline SgComputedGotoStmt(SgExpression &expr;, SgLabel &label;);
  inline void addLabel(SgLabel &label;);
  inline SgExpression *exp();
  inline void setExp(SgExpression &exp;);
  inline ~SgComputedGotoStmt();
};
```

#### Члены класа

`**SgComputedGotoStmt**`**(SgExpression &expr;, SgLabel &label;)**

document me

`void **addLabel**`**(SgLabel &label;)**

document me

`SgExpression ***exp**`**()**

document me

`void **setExp**`**(SgExpression &exp;)**

document me

#### Примеры
[[8 Dump Info - doGoToStmt]]








