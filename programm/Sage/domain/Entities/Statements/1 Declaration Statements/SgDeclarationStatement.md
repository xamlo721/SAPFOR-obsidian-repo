Представляет базовый класс для операторов объявления.

```cpp
class  **SgDeclarationStatement**: public SgStatement {
  // Declaration class
  // abstract class
public:
  inline SgDeclarationStatement(int variant);
  inline ~SgDeclarationStatement();
  
  inline SgExpression *varList();
  inline int numberOfVars();
  inline SgExpression *var(int i);
  inline void deleteVar(int i);
  inline void deleteTheVar(SgExpression &var;);
  inline void addVar(SgExpression &exp;);
};
```

#### Члены класса

`**SgDeclarationStatement**`**(int variant)**

document me

`SgExpression ***varList**`**()**

document me

`int **numberOfVars**`**()**

document me

`SgExpression ***var**`**(int i)**

document me

`void **deleteVar**`**(int i)**

document me

`void **deleteTheVar**`**(SgExpression &var;)**

document me

`void **addVar**`**(SgExpression &exp;)**

document me


