Представляет операторы выражений языка Си.
```cpp
class  **SgCExpStmt**: public SgExecutableStatement {
  // C non-control expression Statment
  // variant == EXPR_STMT_NODE
public:
  inline SgCExpStmt(SgExpression &exp;);
  inline SgCExpStmt(SgExpression &lhs;, SgExpression &rhs;);
  inline SgExpression *expr();  // the expression
  inline void replaceExpression(SgExpression &e;); // replace exp with e
  inline ~SgCExpStmt();
};
```
#### Члены класса

`**SgCExpStmt**`**(SgExpression &exp;)**

document me

`**SgCExpStmt**`**(SgExpression &lhs;, SgExpression &rhs;)**

document me

`SgExpression ***expr**`**()**

document me

`void **replaceExpression**`**(SgExpression &e;)**

document me

#### Примеры
[[4 Instrument - InsertFCallNode]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]



