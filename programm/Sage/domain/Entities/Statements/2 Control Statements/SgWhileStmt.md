Представляет собой оператор C while().

```cpp
class  **SgWhileStmt**: public SgStatement {
  // for C while()
  // variant = WHILE_NODE
public:
  inline SgWhileStmt(int variant);
  inline SgWhileStmt(SgExpression &cond;, SgStatement &body;);
  inline SgExpression *conditional();      // the while test
  inline void replaceBody(SgStatement &s;); // new body = s and lex successors.
  inline ~SgWhileStmt();
};
```

#### Члены класса
`**SgWhileStmt**`**(int variant)**

document me

`**SgWhileStmt**`**(SgExpression &cond;, SgStatement &body;)**

document me

`SgExpression ***conditional**`**()**

document me

`void **replaceBody**`**(SgStatement &s;)**

document me

####  Примеры
[[2 Restructure - addStuffToProgram]]
[[6 Dump Info - doLoopStmts]]

