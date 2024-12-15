Представляет собой объявления структуры Fortran 90.

```cpp
class **SgStructureDeclStmt**: public SgDeclarationStatement {
  // Fortran 90 structure declaration statement
  // variant == STRUCT_DECL
public:
  SgStructureDeclStmt(SgSymbol &name;, SgExpression &attributes;, 
                      SgStatement &body;);
  ~SgStructureDeclStmt();
};
```
#### Члены класса
`**SgStructureDeclStmt**`**(SgSymbol &name;, SgExpression &attributes;, SgStatement &body;)**

document me

`int **isPrivate**`**()**

document me

`int **isPublic**`**()**

document me

`int **isSequence**`**()**

document me

#### Примеры
[[9 Dump Info - doVarDecl]]