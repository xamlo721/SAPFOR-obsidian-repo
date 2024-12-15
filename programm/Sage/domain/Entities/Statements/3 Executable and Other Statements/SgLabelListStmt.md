Представляет инструкции Fortran, содержащие списки меток.
```cpp
class **SgLabelListStmt**: public SgExecutableStatement {
  // the fortran
  // statements containg a list of labels
public:
  SgLabelListStmt(int variant);
  int numberOfTargets();
  SgExpression *labelList();
  void setLabelList(SgExpression &labelList;);
};
```

#### Члены класса

`**SgLabelListStmt**`**(int variant)**

document me

`int **numberOfTargets**`**()**

document me

`SgExpression ***labelList**`**()**

document me

`void **setLabelList**`**(SgExpression &labelList;)**

document me

`SgStatement ***target**`**(int i)**

document me

