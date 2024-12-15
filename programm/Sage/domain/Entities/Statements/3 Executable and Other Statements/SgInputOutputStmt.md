Представляет инструкции Fortran read, write и print.

```cpp
class **SgInputOutputStmt**: public SgIOStmt {
  // fortran input and output statements
  // variant = READ_STAT, WRITE_STATE, PRINT_STAT
public:
  inline SgInputOutputStmt(int variant, SgExpression &specList;, 
                           SgExpression &itemList;);
  inline SgExpression *specList();
  inline void setSpecList(SgExpression &specList;);
  inline SgExpression *itemList();
  inline void setItemList(SgExpression &itemList;);
  inline ~SgInputOutputStmt();
};
```

#### Члены класса

`**SgInputOutputStmt**`**(int variant, SgExpression &specList;, SgExpression &itemList;)**

document me

`SgExpression ***specList**`**()**

document me

`void **setSpecList**`**(SgExpression &specList;)**

document me

`SgExpression ***itemList**`**()**

document me

`void **setItemList**`**(SgExpression &itemList;)**

document me

#### Примеры
[[7 Dump Info - doIOStmts]]