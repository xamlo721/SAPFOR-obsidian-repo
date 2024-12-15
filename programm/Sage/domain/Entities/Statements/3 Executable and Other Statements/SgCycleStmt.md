Представляет инструкции цикла Fortran 90.

```cpp
class  **SgCycleStmt**: public SgExecutableStatement {
  // the fortran 90 cycle statement
  // variant == CYCLE_STMT
public:
  inline SgCycleStmt(SgSymbol &symbol;);
  inline SgSymbol *constructName();  // the name of the loop to cycle
  inline void setConstructName(SgSymbol &constructName;);
  inline ~SgCycleStmt();
};
```

#### Члены класса

`**SgCycleStmt**`**(SgSymbol &symbol;)**

document me

`SgSymbol ***constructName**`**()**

document me

`void **setConstructName**`**(SgSymbol &constructName;)**

document me
