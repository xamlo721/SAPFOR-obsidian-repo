Представляет собой Fortran инструкцию call.

```cpp
class  **SgCallStmt**: public SgExecutableStatement {
  // the fortran call
  // variant == PROC_STAT
public:
  SgCallStmt(SgSymbol &name;, SgExpression &args;);
  SgCallStmt(SgSymbol &name;);
  SgSymbol *name();    // name of subroutine being called
  int numberOfArgs();  // the number of arguement expressions
  void  addArg(SgExpression &arg;);
  SgExpression *arg(int i); // the i-th argument expression
  ~SgCallStmt();
};
```

#### Члены класса

`**SgCallStmt**`**(SgSymbol &name;, SgExpression &args;)**

document me

`**SgCallStmt**`**(SgSymbol &name;)**

document me

`SgSymbol ***name**`**()**

`int **numberOfArgs**`**()**

document me

`void **addArg**`**(SgExpression &arg;)**

document me

`SgExpression ***arg**`**(int i)**

document me

`int **numberOfVarsUsed**`**()**

document me

`SgExpression ***varsUsed**`**(int i)**

document me

`int **numberOfVarsMod**`**()**

document me

`SgExpression ***varsMod**`**(int i)**

document me
#### Примеры
[[2 Restructure - addStuffToProgram]]
[[4 Instrument - InsertFCallNode]]
[[3 Dump Info - classifyStatements]]



