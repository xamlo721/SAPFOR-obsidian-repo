Представляет списки объявлений переменных для всех языков.

```cpp
class  **SgVarListDeclStmt**: public SgDeclarationStatement {
  // Declaration Statement
  // variant == INTENT_STMT, OPTIONAL_STMT, SAVE_STMT, PUBLIC_STMT,
  // PRIVATE_STMT, EXTERNAL_STAT, INTRINSIC_STAT, DIM_STAT, 
  // ALLOCATABLE_STAT, POINTER_STAT, TARGET_STAT, MODULE_PROC_STMT
public:
  SgVarListDeclStmt(int variant, SgExpression &symbolRefList;);
  SgVarListDeclStmt(int variant, SgSymbol &symbolList;, SgStatement &scope;);

  inline ~SgVarListDeclStmt();
  
  inline int numberOfSymbols();
  inline SgSymbol *symbol(int i);
  inline void appendSymbol(SgSymbol &symbol;);
  inline void deleteSymbol(int i);
  inline void deleteTheSymbol(SgSymbol &symbol;);
};
```

#### Члены класса
`**SgVarListDeclStmt**`**(int variant, SgExpression &symbolRefList;)**

document me

`**SgVarListDeclStmt**`**(int variant, SgSymbol &symbolList;, SgStatement &scope;)**

document me

`int **numberOfSymbols**`**()**

document me

`SgSymbol ***symbol**`**(int i)**

document me

`void **appendSymbol**`**(SgSymbol &symbol;)**

document me

`void **deleteSymbol**`**(int i)**

document me

`void **deleteTheSymbol**`**(SgSymbol &symbol;)**

document me

#### Примеры
[[9 Dump Info - doVarDecl]]
