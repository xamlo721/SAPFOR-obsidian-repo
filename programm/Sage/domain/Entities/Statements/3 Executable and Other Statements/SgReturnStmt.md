Представляет собой оператор return для всех языков.

```cpp
class  **SgReturnStmt**: public SgExecutableStatement {
  // the return (expr) node
  // variant == RETURN_NODE//RETURN_STAT
public:
  SgReturnStmt(SgExpression &returnValue;);
  SgReturnStmt();
  inline SgExpression *returnValue();
  inline void setReturnValue(SgExpression &retVal;);
  inline ~SgReturnStmt();
};
```

#### Члены класса

`**SgReturnStmt**`**(SgExpression &returnValue;)**

document me

`**SgReturnStmt**`**()**

document me

`SgExpression ***returnValue**`**()**

document me

`void **setReturnValue**`**(SgExpression &retVal;)**

document me

#### Примеры
[[2 Restructure - addStuffToProgram]]