Представляет собой инструкцию goto, назначенную Fortran.

```cpp
class **SgAssignedGotoStmt**: public SgLabelListStmt {
  // the fortran 
  // variant == ASSGOTO_NODE
public:
  SgAssignedGotoStmt(SgSymbol &symbol;, SgExpression &labelList;);
  SgSymbol *symbol();
  void setSymbol(SgSymbol &symb;);
  ~SgAssignedGotoStmt();
};
```

#### Члены класса

`**SgAssignedGotoStmt**`**(SgSymbol &symbol;, SgExpression &labelList;)**

document me

`SgSymbol ***symbol**`**()**

document me

`void **setSymbol**`**(SgSymbol &symb;)**

document me

#### Примеры
[[8 Dump Info - doGoToStmt]]