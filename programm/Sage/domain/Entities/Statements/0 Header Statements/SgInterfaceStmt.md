Представляет инструкции операторского интерфейса Fortran 90.

```cpp
class  **SgInterfaceStmt**: public SgStatement {
  // Fortran 90 Operator Interface Statement
  // variant == INTERFACE_STMT
public:
  SgInterfaceStmt(SgSymbol &name;, SgStatement &body;, SgStatement &scope;);
  ~SgInterfaceStmt();
  
  SgSymbol *interfaceName();               // interface name if given
  int setName(SgSymbol &symbol;);           // set interface name 
  
  int numberOfSpecificationStmts();
  
  SgStatement *specificationStmt(int i);
  
  int isSymbolInScope(SgSymbol &symbol;);
  int isSymbolDeclaredHere(SgSymbol &symbol;);
};
```

#### Члены класса
`**SgInterfaceStmt**`**(SgSymbol &name;, SgStatement &body;, SgStatement &scope;)**

document me

`SgSymbol ***interfaceName**`**()**

document me

`int **setName**`**(SgSymbol &symbol;)**

document me

`int **numberOfSpecificationStmts**`**()**

document me

`SgStatement ***specificationStmt**`**(int i)**

document me

`int **isSymbolInScope**`**(SgSymbol &symbol;)**

document me

`int **isSymbolDeclaredHere**`**(SgSymbol &symbol;)**

document me