
Представляет функции для всех языков.
```cpp
class  **SgFuncHedrStmt**: public SgProcHedrStmt {
  // Fortran and C function.
  // variant == FUNC_HEDR
public:
  inline SgFuncHedrStmt(SgSymbol &name;, SgStatement &Body;);
  inline SgFuncHedrStmt(SgSymbol &name;, SgType &type;, SgStatement &Body;);
  inline SgFuncHedrStmt(SgSymbol &name;, SgSymbol &resultName;, SgType &type;, 
                        SgStatement &Body;);
  inline SgFuncHedrStmt(SgSymbol &name;);
  inline SgFuncHedrStmt(SgSymbol &name;, SgExpression *exp);
  inline SgFuncHedrStmt(char *name);
  inline ~SgFuncHedrStmt();
  
  inline SgSymbol *resultName();  // name of result variable.;
  int  setResultName(SgSymbol &symbol;); // set name of result variable.;
  
  inline SgType *returnedType();  // type of returned value
  inline void setReturnedType(SgType &type;);  // set type of returned value
};
```

#### Члены класса

document me
`**SgFuncHedrStmt**`**(SgSymbol &name;, SgStatement Body)**


document me
`**SgFuncHedrStmt**`**(SgSymbol &name;, SgType &type;, SgStatement Body)**


document me
`**SgFuncHedrStmt**`**(SgSymbol &name;, SgSymbol &resultName;, SgType &type;, SgStatement Body)**


document me
`**SgFuncHedrStmt**`**(SgSymbol &name;)**


document me
`**SgFuncHedrStmt**`**(char *name)**


document me
`SgSymbol ***resultName**`**()**


document me
`int **setResultName**`**(SgSymbol &symbol;)**


document me
`SgType ***returnedType**`**()**


document me
`void **setReturnedType**`**(SgType &type;)**


#### Использование


#### Примеры
[[2 Restructure - addStuffToProgram]]
[[16 Instrument - inMethodOfTheElement]]
[[17 Instrument - whichFunctionAmI]]
[[4 Dump Info - doRoutineHeader]]

