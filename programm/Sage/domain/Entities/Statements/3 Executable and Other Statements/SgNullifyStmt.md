Представляет собой инструкцию инициализации указателя Fortran.

```cpp
class  **SgNullifyStmt**: public SgExecutableStatement {
  // Fortran pointer initialization statement
  // variant == NULLIFY_STMT 
public:
  inline SgNullifyStmt(SgExpression &objectList;);
  inline ~SgNullifyStmt();
  inline SgExpression *nullifyList();
  inline void setNullifyList(SgExpression &nullifyList;);
};
```

#### Члены класса
`**SgNullifyStmt**`**(SgExpression &objectList;)**

document me

`SgExpression ***nullifyList**`**()**

document me

`void **setNullifyList**`**(SgExpression &nullifyList;)**

document me
