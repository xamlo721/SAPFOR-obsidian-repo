Представляет инструкции модуля Fortran 90.
```cpp
Represents Fortran 90 `module` statements.

class  **SgModuleStmt**: public SgStatement {
  // Fortran 90 Module statement
  // variant ==  MODULE_STMT
public:
  SgModuleStmt(SgSymbol &moduleName;, SgStatement &body;);
  SgModuleStmt(SgSymbol &moduleName;);
  ~SgModuleStmt();
  
  SgSymbol *moduleName();               // module name 
  void setName(SgSymbol &symbol;);        // set module name 
  
  int numberOfSpecificationStmts();
  int numberOfRoutinesDefined();
  int numberOfFunctionsDefined();
  int numberOfSubroutinesDefined();
  
  SgStatement *specificationStmt(int i);
  SgStatement *routine(int i);
  SgStatement *function(int i);
  SgStatement *subroutine(int i);
  
  int isSymbolInScope(SgSymbol &symbol;);
  int isSymbolDeclaredHere(SgSymbol &symbol;);
  
  SgSymbol &addVariable;(SgType &T;, char *name); 
                                        //add a declaration for new variable
  
  SgStatement *addCommonBlock(char *blockname, int noOfVars,
                              SgSymbol *Vars); // add a new common block
};
```

#### Члены класса

`**SgModuleStmt**`**(SgSymbol &moduleName;, SgStatement &body;)**

document me

`**SgModuleStmt**`**(SgSymbol &moduleName;)**

document me

`SgSymbol ***moduleName**`**()**

document me

`void **setName**`**(SgSymbol &symbol;)**

document me

`int **numberOfSpecificationStmts**`**()**

document me

`int **numberOfRoutinesDefined**`**()**

document me

`int **numberOfFunctionsDefined**`**()**

document me

`int **numberOfSubroutinesDefined**`**()**

document me

`SgStatement ***specificationStmt**`**(int i)**

document me

`SgStatement ***routine**`**(int i)**

document me

`SgStatement ***function**`**(int i)**

document me

`SgStatement ***subroutine**`**(int i)**

document me

`int **isSymbolInScope**`**(SgSymbol &symbol;)**

document me

`int **isSymbolDeclaredHere**`**(SgSymbol &symbol;)**

document me

`SgSymbol &**addVariable**`**(SgType &T;, char *name)**

document me

`SgStatement ***addCommonBlock**`**(char *blockname, int noOfVars, SgSymbol *Vars)**

document me