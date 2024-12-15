Представляет собой оператор case option.

```cpp
class **SgCaseOptionStmt**: public SgStatement {
  // Fortran case option statement
  // variant == CASE_NODE
public:
  inline SgCaseOptionStmt(SgExpression &caseRangeList;, SgStatement &body;, 
                          SgSymbol &constructName;);
  inline SgCaseOptionStmt(SgExpression &caseRangeList;, SgStatement *body, 
                          SgSymbol &constructName;);
  inline SgCaseOptionStmt(SgExpression &caseRangeList;, SgStatement *body, 
                          SgSymbol *constructName);
  inline ~SgCaseOptionStmt();
  
  inline SgExpression *caseRangeList();
  inline void setCaseRangeList(SgExpression &caseRangeList;);
  inline SgExpression *caseRange(int i);
  inline void setCaseRange(SgExpression &caseRange;);
  inline SgStatement *body();
  inline void setBody(SgStatement &body;);
};
```
#### Члены класса
`**SgCaseOptionStmt**`**(SgExpression &caseRangeList;, SgStatement &body;, SgSymbol &constructName;)**

document me

`SgExpression ***caseRangeList**`**()**

document me

`void **setCaseRangeList**`**(SgExpression &caseRangeList;)**

document me

`SgExpression ***caseRange**`**(int i)**

document me

`void **setCaseRange**`**(int i, SgExpression &caseRange;)**

document me

`SgStatement ***body**`**()**

document me

`void **setBody**`**(SgStatement &body;)**

document me