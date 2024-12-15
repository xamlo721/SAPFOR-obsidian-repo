Представляет инструкции по использованию модуля Fortran 90.

```cpp
class **SgUseStmt**: public SgDeclarationStatement {
  // Fortran 90 module usuage statement
  // variant = USE_STMT
public:
  SgUseStmt(SgSymbol &moduleName;, SgExpression &renameList;, SgStatement &scope;);
  // renameList must be a list of low-level nodes of variant RENAME_NODE
  ~SgUseStmt();
  
  int isOnly();
  SgSymbol *moduleName();
  void setModuleName(SgSymbol &moduleName;);
  int numberOfRenames();
  SgExpression *renameNode(int i);
  void  addRename(SgSymbol &localName;, SgSymbol &useName;);
  void  addRenameNode(SgExpression &renameNode;);
  void  deleteRenameNode(int i);
  void deleteTheRenameNode(SgExpression &renameNode;);
};
```


#### Члены Класса

`**SgUseStmt**`**(SgSymbol &moduleName;, SgExpression &renameList;, SgStatement &scope;)**

document me

`int **isOnly**`**()**

document me

`SgSymbol ***moduleName**`**()**

document me

`void **setModuleName**`**(SgSymbol &moduleName;)**

document me

`int **numberOfRenames**`**()**

document me

`SgExpression ***renameNode**`**(int i)**

document me

`void **addRename**`**(SgSymbol &localName;, SgSymbol &useName;)**

document me

`void **addRenameNode**`**(SgExpression &renameNode;)**

document me

`void **deleteRenameNode**`**(int i)**

document me

`void **deleteTheRenameNode**`**(SgExpression &renameNode;)**

document me