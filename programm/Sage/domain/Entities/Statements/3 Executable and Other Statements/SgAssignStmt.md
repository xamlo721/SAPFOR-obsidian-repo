Представляет собой инструкции присваивания на Fortran.

```cpp
class **SgAssignStmt**: public SgExecutableStatement {
  // Fortran assignment Statment
  // variant == ASSIGN_STAT
public:
  inline SgAssignStmt(int variant);
  inline SgAssignStmt(SgExpression &lhs;, SgExpression &rhs;);
  inline SgExpression *lhs();  // the left hand side
  inline SgExpression *rhs();  // the right hand side
  inline void replaceLhs(SgExpression &e;); // replace lhs with e
  inline void replaceRhs(SgExpression &e;); // replace rhs with e
};
```

#### Члены класса

`**SgAssignStmt**`**(int variant)**

document me

`**SgAssignStmt**`**(SgExpression &lhs;, SgExpression &rhs;)**

document me

`SgExpression ***lhs**`**()**

document me

`SgExpression ***rhs**`**()**

document me

`void **replaceLhs**`**(SgExpression &e;)**

document me

`void **replaceRhs**`**(SgExpression &e;)**

document me

`SgExpression ***varReferenced**`**()**

document me

`SgExpression ***varUsed**`**()**

document me

`SgExpression ***varDefined**`**()**

document me

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[3 Dump Info - classifyStatements]]



