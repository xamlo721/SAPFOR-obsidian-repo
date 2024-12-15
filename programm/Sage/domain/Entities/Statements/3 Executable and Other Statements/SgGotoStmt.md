Представляет собой переход для всех языков.
```cpp
class  **SgGotoStmt**: public SgExecutableStatement {
  // the fortran or C goto
  // variant == GOTO_NODE
public:
  inline SgGotoStmt(SgLabel &label;);
  inline SgLabel *branchLabel();
  inline ~SgGotoStmt();
};
```

#### Члены класса 

`**SgGotoStmt**`**(SgLabel &label;)**

document me

`SgLabel ***branchLabel**`**()**

document me

`SgStatement ***target**`**()**

document me


#### Примеры
[[8 Dump Info - doGoToStmt]]