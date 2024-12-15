Представляет собой арифметический оператор if на языке Фортран.

```cpp
class  **SgArithIfStmt**: public SgStatement {
  // For Fortran Arithementic if
  // variant == ARITHIF_NODE
public:
  inline SgArithIfStmt(int variant);
  inline SgArithIfStmt(SgExpression &cond;, SgLabel &llabel;, 
                       SgLabel &elabel;, SgLabel &glabel;);
  inline SgExpression *conditional();
  inline void set_conditional(SgExpression &cond;);
  inline SgExpression *label(int i);  // the <, ==, and > goto labels. 
                                      // in order 0->2.
  inline void setLabel(SgLabel &label;);
  inline ~SgArithIfStmt();
};
```

#### Члены класса

`**SgArithIfStmt**`**(int variant)**

document me

`**SgArithIfStmt**`**(SgExpression &cond;, SgLabel &llabel;, SgLabel &elabel;, SgLabel &glabel;)**

document me

`SgExpression ***conditional**`**()**

document me

`void **set_conditional**`**(SgExpression &cond;)**

document me

`SgExpression ***label**`**(int i)**

document me

`void **setLabel**`**(SgLabel &label;)**

document me

#### Примеры
[[5 Dump Info - doIfStmts]]