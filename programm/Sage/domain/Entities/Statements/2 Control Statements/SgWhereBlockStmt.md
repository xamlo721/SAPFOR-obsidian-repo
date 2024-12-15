Представляет собой оператор Fortran where .. elsewhere.

```cpp
class  **SgWhereBlockStmt**: public SgIfStmt {
  // fortran Where - Elsewhere stmt
  // variant == WHERE_BLOCK_STMT
public:
  SgWhereBlockStmt(SgExpression &cond;, SgStatement &trueBody;, 
                   SgStatement &falseBody;);
  ~SgWhereBlockStmt();
};
```

#### Члены класса
`**SgWhereBlockStmt**`**(SgExpression &cond;, SgStatement &trueBody;, SgStatement &falseBody;)**

document me