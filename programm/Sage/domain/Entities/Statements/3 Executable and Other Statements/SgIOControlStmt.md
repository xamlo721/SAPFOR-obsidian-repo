Представляет инструкции Fortran open, close, inquire, backspace, rewind, endfile и format на языке Fortran.
```cpp
class **SgIOControlStmt**: public SgExecutableStatement {
  // fortran input/output control and editing statements
  // variant = OPEN_STAT, CLOSE_STAT, INQUIRE_STAT, BACKSPACE_STAT,
  // REWIND_STAT, ENDFILE_STAT, FORMAT_STAT
public:
  SgIOControlStmt(int variant, SgExpression &controlSpecifierList;);
  inline SgExpression *controlSpecList();
  inline void setControlSpecList(SgExpression &controlSpecList;);
  inline ~SgIOControlStmt();
};
```

#### Члены класса

`**SgIOControlStmt**`**(int variant, SgExpression &controlSpecifierList;)**

document me

`SgExpression ***controlSpecList**`**()**

document me

`void **setControlSpecList**`**(SgExpression &controlSpecList;)**

document me


#### Примеры
[[7 Dump Info - doIOStmts]]