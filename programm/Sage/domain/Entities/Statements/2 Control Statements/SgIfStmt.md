Представляет собой операторы C if и Fortran if .. then .. else.

```cpp
class  **SgIfStmt**: public SgStatement {
  // For Fortran if then else and C  if()
  // variant == IF_NODE
public:
  inline SgIfStmt(int variant);
  inline SgIfStmt(SgExpression &cond;, SgStatement &trueBody;, SgStatement &falseBody;,
                  SgSymbol &construct;_name);
  inline SgIfStmt(SgExpression &cond;, SgStatement &trueBody;, SgStatement &falseBody;);
  inline SgIfStmt(SgExpression &cond;, SgStatement &trueBody;);
  inline SgStatement *trueBody();      // the first stmt in the True clause
  // SgBlock is needed? 
  inline SgStatement *trueBody(int i); // i-th stmt in True clause, i=0,1,...
  inline SgStatement *falseBody();     // the first stmt in the False
  inline SgStatement *falseBody(int i);// i-th stmt of the body, i=0,1,...
  inline SgExpression *conditional();  // the while test
  inline SgSymbol *construct_name();
  inline void replaceTrueBody(SgStatement &s;);// new body=s and lex successors.
  inline void replaceFalseBody(SgStatement &s;);//new body=s and lex successors.
  inline ~SgIfStmt();
};
```

#### Члены класса
`**SgIfStmt**`**(int variant)**

document me

`**SgIfStmt**`**(SgExpression &cond;, SgStatement &trueBody;, SgStatement &falseBody;, SgSymbol &construct;_name)**

document me

`**SgIfStmt**`**(SgExpression &cond;, SgStatement &trueBody;, SgStatement &falseBody;)**

document me

`**SgIfStmt**`**(SgExpression &cond;, SgStatement &trueBody;)**

document me

`SgStatement ***trueBody**`**()**

document me

`SgStatement ***trueBody**`**(int i)**

document me

`SgStatement ***falseBody**`**()**

document me

`SgStatement ***falseBody**`**(int i)**

document me

`SgExpression ***conditional**`**()**

document me

`SgSymbol ***construct_name**`**()**

document me

`void **replaceTrueBody**`**(SgStatement &s;)**

document me

`void **replaceFalseBody**`**(SgStatement &s;)**

document me

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[5 Dump Info - doIfStmts]]
