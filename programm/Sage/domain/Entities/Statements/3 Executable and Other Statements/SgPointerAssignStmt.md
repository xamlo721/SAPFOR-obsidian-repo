Представляет собой инструкции присваивания указателя Fortran.

```cpp
class  **SgPointerAssignStmt**: public SgAssignStmt {
  // Fortran  pointer assignment statement
  // variant == POINTER_ASSIGN_STAT
public:
  inline SgPointerAssignStmt(SgExpression lhs, SgExpression rhs);
  inline ~SgPointerAssignStmt();
};
```

#### Члены класса

`**SgPointerAssignStmt**`**(SgExpression lhs, SgExpression rhs)**

document me
