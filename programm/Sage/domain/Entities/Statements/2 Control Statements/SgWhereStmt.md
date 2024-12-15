Представляет оператор where на Fortran языке.

```cpp
class  **SgWhereStmt**: public SgLogIfStmt {
  // fortran Where stmt
  // variant == WHERE_NODE
public:
  inline SgWhereStmt(SgExpression &cond;, SgStatement &body;);
  inline ~SgWhereStmt();
};
```
#### Члены класса
`**SgWhereStmt**`**(SgExpression &cond;, SgStatement &body;)**

document me


