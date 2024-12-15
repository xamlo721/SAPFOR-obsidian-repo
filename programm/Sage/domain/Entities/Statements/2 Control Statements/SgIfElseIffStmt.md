Представляет собой оператор Fortran if .. then .. elseif.

```cpp
class  **SgIfElseIfStmt**: public SgIfStmt {
  // For Fortran if then elseif .. elseif ... case
  // variant == ELSEIF_NODE
public:
  SgIfElseIfStmt(SgExpression &condList;, SgStatement &blockList;,
                 SgSymbol &constructName;);
  int numberOfConditionals();       // the number of conditionals
  SgStatement *body(int b);          // block b
  void setBody(int b);              // sets block 
  SgExpression *conditional(int i); // the i-th conditional
  void setConditional(int i);       // sets the i-th conditional
  void addClause(SgExpression &cond;, SgStatement &st);
  void removeClause(int b);          // removes block b and it's conditional
  ~SgIfElseIfStmt();
};
```
#### Члены класса

`**SgIfElseIfStmt**`**(SgExpression &condList;, SgStatement &blockList;, SgSymbol &constructName;)**

document me

`int **numberOfConditionals**`**()**

document me

`SgStatement ***body**`**(int b)**

document me

`void **setBody**`**(int b)**

document me

`SgExpression ***conditional**`**(int i)**

document me

`void **setConditional**`**(int i)**

document me

`void **addClause**`**(SgExpression &cond;, SgStatement )**

document me

`void **removeClause**`**(int b)**

document me




