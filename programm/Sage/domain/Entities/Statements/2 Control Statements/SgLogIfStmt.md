Представляет собой логический оператор if на языке Фортран.

```cpp
class  **SgLogIfStmt**: public SgStatement {
  // For Fortran logical if  - only one body statement allowed
  // variant == LOGIF_NODE
public:
  inline SgLogIfStmt(int variant);
  inline SgLogIfStmt(SgExpression &cond;, SgStatement &s;);
  inline SgStatement *body();  // returns reference to first stmt in the body
  inline SgExpression *conditional();  // the while test
  // check if the statement s is a single statement. 
  inline void setBody(SgStatement &s;); // new body = s 
  // this code won't work, since after the addition false
  //   clause, it should become SgIfThenElse statement.
  inline void addFalseClause(SgStatement &s;); // make it into if-then-else
  inline SgIfStmt *convertLogicIf();
  inline ~SgLogIfStmt();
};
```

#### Члены класса

`**SgLogIfStmt**`**(int variant)**

document me

`**SgLogIfStmt**`**(SgExpression &cond;, SgStatement &s;)**

document me

`SgStatement ***body**`**()**

document me

`SgExpression ***conditional**`**()**

document me

`void **setBody**`**(SgStatement &s;)**

document me

`void **addFalseClause**`**(SgStatement &s;)**

document me

`SgIfStmt ***convertLogicIf**`**()**

document me

#### Примеры
[[5 Dump Info - doIfStmts]]
