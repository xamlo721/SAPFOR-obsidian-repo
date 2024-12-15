Представляет инструкции C do...while и Fortran dowhile.

```cpp
class  **SgDoWhileStmt**: public SgWhileStmt {
  // For Fortran  dowhile().. and C do {....) while();
  // variant = DO_WHILE_NODE
public:
  inline SgDoWhileStmt(SgExpression &cond;, SgStatement &body;);
  inline ~SgDoWhileStmt();
};
```

#### Члены класса

`**SgDoWhileStmt**`**(SgExpression &cond;, SgStatement &body;)**

document me