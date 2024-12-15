Представляет программные блоки на языке Фортран.

```cpp
class  **SgProgHedrStmt**: public SgStatement {
  // fortran Program block
  // variant == PROG_HEDR
public:
  inline SgProgHedrStmt(PTR_BFND bif);
  inline SgProgHedrStmt(int variant);
  inline SgProgHedrStmt(SgSymbol &name;, SgStatement &Body;);
  inline SgProgHedrStmt(SgSymbol &name;);
  inline SgProgHedrStmt(char *name);
  inline SgSymbol &name;();
  inline void setName(SgSymbol &symbol;); // set program name 

  inline int numberOfFunctionsCalled();  // the number of functions called
  inline SgSymbol *calledFunction(int i);// the i-th called function
  inline int numberOfStmtFunctions();   // the number of statement funcions;
  inline SgStatement *statementFunc(int i); // the i-th statement function;
  inline int numberOfEntryPoints();     // the number of entry points;
  inline SgStatement *entryPoint(int i); // the i-th entry point;
  inline int numberOfParameters();       // the number of parameters;       
  inline SgSymbol *parameter(int i);     // the i-th parameter  
  inline int numberOfSpecificationStmts();
  inline SgStatement *specificationStmt(int i);
  inline int numberOfExecutionStmts();
  inline SgStatement *executionStmt(int i);
  inline int numberOfInternalFunctionsDefined();
  inline SgStatement *internalFunction(int i);
  inline int numberOfInternalSubroutinesDefined();
  inline SgStatement *internalSubroutine(int i);
  inline int numberOfInternalSubProgramsDefined();
  inline SgStatement *internalSubProgram(int i);
  
  inline int isSymbolInScope(SgSymbol &symbol;);
  inline int isSymbolDeclaredHere(SgSymbol &symbol;);
  
  // global analysis data
  
  inline int numberOfVarsUsed();  // list of used variable access sections
  inline SgExpression *varsUsed(int i); // i-th var used section descriptor
  inline int numberofVarsMod();   // list of modifed variable access sections
  inline SgExpression *varsMod(int i);   // i-th var mod section descriptor
  inline ~SgProgHedrStmt();
};
```
#### Члены Класса 
document me
`**SgProgHedrStmt**`**(PTR_BFND bif)**


document me
`**SgProgHedrStmt**`**(int variant)**


document me
`**SgProgHedrStmt**`**(SgSymbol &name;, SgStatement Body)**


document me
`**SgProgHedrStmt**`**(SgSymbol &name;)**


document me
`**SgProgHedrStmt**`**(char *name)**


document me
`SgSymbol &**name**`**()**


document me
`void **setName**`**(SgSymbol &symbol;)**


document me
`int **numberOfFunctionsCalled**`**()**


document me
`SgSymbol ***calledFunction**`**(int i)**


document me
`int **numberOfStmtFunctions**`**()**


document me
`SgStatement ***statementFunc**`**(int i)**


document me
`int **numberOfEntryPoints**`**()**


document me
`SgStatement ***entryPoint**`**(int i)**


document me
`int **numberOfParameters**`**()**


document me
`SgSymbol ***parameter**`**(int i)**


document me
`int **numberOfSpecificationStmts**`**()**


document me
`SgStatement ***specificationStmt**`**(int i)**


document me
`int **numberOfExecutionStmts**`**()**


document me
`SgStatement ***executionStmt**`**(int i)**


document me
`int **numberOfInternalFunctionsDefined**`**()**


document me
`SgStatement ***internalFunction**`**(int i)**


document me
`int **numberOfInternalSubroutinesDefined**`**()**


document me
`SgStatement ***internalSubroutine**`**(int i)**


document me
`int **numberOfInternalSubProgramsDefined**`**()**


document me
`SgStatement ***internalSubProgram**`**(int i)**


document me
`int **isSymbolInScope**`**(SgSymbol &symbol;)**


document me
`int **isSymbolDeclaredHere**`**(SgSymbol &symbol;)**


document me
`int **numberOfVarsUsed**`**()**


document me
`SgExpression ***varsUsed**`**(int i)**


document me
`int **numberofVarsMod**`**()**


document me
`SgExpression ***varsMod**`**(int i)**


#### Использование


#### Примеры
[[4 Dump Info - doRoutineHeader]]