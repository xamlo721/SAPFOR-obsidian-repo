Представляет собой объявления функций оператора Fortran.

```cpp
class  **SgStmtFunctionStmt**: public SgDeclarationStatement {
  // Fortran statement function declaration
  // variant == STMTFN_DECL
public:        
  SgStmtFunctionStmt(SgSymbol &name;, SgExpression &args;, SgStatement Body);
  ~SgStmtFunctionStmt();
  SgSymbol *name();
  void setName(SgSymbol &name;);
  SgType *type();
  int numberOfParameters();       // the number of parameters
  SgSymbol *parameter(int i);     // the i-th parameter
};
```

#### Члены класса
`**SgStmtFunctionStmt**`**(SgSymbol &name;, SgExpression &args;, SgStatement Body)**

document me

`SgSymbol ***name**`**()**

document me

`void **setName**`**(SgSymbol &name;)**

document me

`SgType ***type**`**()**

document me

`int **numberOfParameters**`**()**

document me

`SgSymbol ***parameter**`**(int i)**

document me