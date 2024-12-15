Представляет Fortran-списки списков объявлений переменных.
```cpp
class **SgNestedVarListDeclStmt**: public SgDeclarationStatement {
  // Declaration statement
  // variant == NAMELIST_STAT, EQUI_STAT, COMM_STAT,
  //            and  PROS_COMM for Fortran M
  // These statements have the format of a list of variable lists. For example,
  // EQUIVALENCE (A, C, D), (B, G, F), ....
public:
  SgNestedVarListDeclStmt(int variant, SgExpression &listOfVarList;);
  // varList must be of low-level variant appropriate to variant. For example,
  // if the variant is COMM_STAT, listOfVarList must be of variant COMM_LIST.
  ~SgNestedVarListDeclStmt();
  
  SgExpression *lists();
  int numberOfLists();
  SgExpression *list(int i);
  void addList(SgExpression &list;);
  void  addVarToList(SgExpression &varRef;);
  void deleteList(int i);
  void deleteTheList(SgExpression &list;);
  void deleteVarInList(int i, SgExpression &varRef;);
  void deleteVarInTheList(SgExpression &list;, SgExpression &varRef;);
};
```
#### Члены класса
`**SgNestedVarListDeclStmt**`**(int variant, SgExpression &listOfVarList;)**

document me

`SgExpression ***lists**`**()**

document me

`int **numberOfLists**`**()**

document me

`SgExpression ***list**`**(int i)**

document me

`SgExpression ***leadingVar**`**(int i)**

document me

`void **addList**`**(SgExpression &list;)**

document me

`void **addVarToList**`**(SgExpression &varRef;)**

document me

`void **deleteList**`**(int i)**

document me

`void **deleteTheList**`**(SgExpression &list;)**

document me

`void **deleteVarInList**`**(int i, SgExpression &varRef;)**

document me

`void **deleteVarInTheList**`**(SgExpression &list;, SgExpression &varRef;)**

document me

#### Примеры
[[9 Dump Info - doVarDecl]]