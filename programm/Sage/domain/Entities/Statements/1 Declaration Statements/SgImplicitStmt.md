Представляет собой неявные объявления типов Fortran.

```cpp
class **SgImplicitStmt**: public SgDeclarationStatement {
  // Fortran implicit type declaration statement
  // variant = IMPL_DECL
public:
  SgImplicitStmt(SgExpression &implicitLists;);
  ~SgImplicitStmt();
  
  int numberOfImplicitTypes();  // the number of implicit types declared;
  SgType *implicitType(int i); // the i-th implicit type
  SgExpression *implicitRangeList(int i) ;
  void  appendImplicitNode(SgExpression &impNode;);
};
```


#### Члены класса
`**SgImplicitStmt**`**(SgExpression &implicitLists;)**

document me

`int **numberOfImplicitTypes**`**()**

document me

`SgType ***implicitType**`**(int i)**

document me

`SgExpression ***implicitRangeList**`**(int i)**

document me

`void **appendImplicitNode**`**(SgExpression &impNode;)**

document me

`void **addImplicitType**`**(SgType Type, char alphabet[])**

document me

`int **deleteImplicitItem**`**(int i)**

document me

`int **deleteTheImplicitItem**`**(SgExpression &implicitItem;)**

document me

#### Примеры
[[9 Dump Info - doVarDecl]]