Представляет константы Фортрана.

```cpp
class **SgParameterStmt**: public SgDeclarationStatement {
  // Fortran constants declaration statement
  // variant = PARAM_DECL
public:
  SgParameterStmt(SgExpression &constants;, SgExpression &values;);
  SgParameterStmt(SgExpression &constantsWithValues;);
  ~SgParameterStmt();
  
  int numberOfConstants();    // the number of constants declared
  
  SgSymbol *constant(int i);  // the i-th variable
  SgExpression *value(int i); // the value of i-th variable
  
  void addConstant(SgSymbol &constant;, SgExpression &value;);
  void deleteConstant(int i);
  void deleteTheConstant(SgSymbol &constant;);
};
```

#### Члены класса
`**SgParameterStmt**`**(SgExpression &constants;, SgExpression &values;)**

document me

`**SgParameterStmt**`**(SgExpression &constantsWithValues;)**

document me

`int **numberOfConstants**`**()**

document me

`SgSymbol ***constant**`**(int i)**

document me

`void **addConstant**`**(SgSymbol &constant;, SgExpression &value;)**

document me

`void **deleteConstant**`**(int i)**

document me

`void **deleteTheConstant**`**(SgSymbol &constant;)**

document me

#### Примеры
[[9 Dump Info - doVarDecl]]

