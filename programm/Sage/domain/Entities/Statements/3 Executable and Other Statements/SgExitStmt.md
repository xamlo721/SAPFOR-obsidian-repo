Represents the Fortran 90 `exit` statements.
```cpp
class  **SgExitStmt**: public SgControlEndStmt {
  // the fortran 90 exit statement
  // variant == EXIT_STMT
public:
  inline SgExitStmt(SgSymbol &construct;_name);
  inline ~SgExitStmt();
  inline SgSymbol *constructName();  // the name of the loop to cycle
  inline void setConstructName(SgSymbol &constructName;);
};
```

#### Члены класса

`**SgExitStmt**`**(SgSymbol &construct;_name)**

document me

`SgSymbol ***constructName**`**()**

document me

`void **setConstructName**`**(SgSymbol &constructName;)**

document me