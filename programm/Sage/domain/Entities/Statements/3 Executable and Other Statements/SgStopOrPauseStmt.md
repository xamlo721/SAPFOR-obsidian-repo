Представляет собой Fortran инструкцию stop.

```cpp
class  **SgStopOrPauseStmt**: public SgExecutableStatement {
  // the fortran stop
  // variant == STOP_STAT
public:
  SgStopOrPauseStmt(int variant, SgExpression *expr);
  SgExpression *exp();
  void setExp(SgExpression &exp;);
  ~SgStopOrPauseStmt();
};
```
#### Члены класса

`**SgStopOrPauseStmt**`**(int variant, SgExpression &expr;)**

document me

`SgExpression ***exp**`**()**

document me

`void **setExp**`**(SgExpression &exp;)**

document me