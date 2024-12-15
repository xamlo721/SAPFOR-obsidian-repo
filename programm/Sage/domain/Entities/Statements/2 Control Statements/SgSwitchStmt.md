Представляет собой оператор C switch и Fortran case.

```cpp
class  **SgSwitchStmt**: public SgStatement {
  // Fortran Case and C  switch();
  // variant == SWITCH_NODE
public:
  inline SgSwitchStmt(SgExpression &selector;, SgStatement &caseOptionList;,
                      SgSymbol &constructName;);
  inline SgSwitchStmt(SgExpression &selector;, SgStatement * caseOptionList,
                      SgSymbol &constructName;);
  inline SgSwitchStmt(SgExpression &selector;, SgStatement * caseOptionList,
                      SgSymbol *constructName);
  inline ~SgSwitchStmt();
  inline SgExpression *selector();  // the switch selector
  inline void setSelector(SgExpression &cond;);
  inline int numberOfCaseOptions();       // the number of cases
  inline SgStatement *caseOption(int i);  // i-th case block
  inline void addCaseOption(SgStatement &caseOption;);
};
```

#### Члены класса
`**SgSwitchStmt**`**(SgExpression &selector;, SgStatement &caseOptionList;, SgSymbol &constructName;)**

document me

`SgExpression ***selector**`**()**

document me

`void **setSelector**`**(SgExpression &cond;)**

document me

`int **numberOfCaseOptions**`**()**

document me

`SgStatement ***caseOption**`**(int i)**

document me

`void **addCaseOption**`**(SgStatement &caseOption;)**

document me


