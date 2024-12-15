Представляет собой инструкции объявления для всех языков.
```cpp
class  **SgVarDeclStmt**: public SgDeclarationStatement {
  // Declaration Statement
  // variant == VAR_DECL
public:
  // varRefValList is a list of low-level nodes of
  // variants VAR_REFs or ARRAY_REFs or ASSIGN_OPs
  inline SgVarDeclStmt(SgExpression &varRefValList;, 
                       SgExpression &attributeList;, SgType &type;);
  inline SgVarDeclStmt(SgExpression &varRefValList;, SgType &type;);
  inline SgVarDeclStmt(SgExpression &varRefValList;);
  inline ~SgVarDeclStmt();
  inline SgType *type();  // the type;
  inline int numberOfAttributesF90(); // the number of F90 attributes;
  // the attributes are: PARAMETER_OP | PUBLIC_OP |
  //    PRIVATE_OP | ALLOCATABLE_OP | EXTERNAL_OP |
  //    OPTIONAL_OP | POINTER_OP | SAVE_OP TARGET_OP
  inline int numberOfSymbols();  // the number of variables declared;        
  inline SgSymbol *symbol(int i);
  
  inline void deleteSymbol(int i);
  inline void deleteTheSymbol(SgSymbol &symbol;);
  inline SgExpression *initialValue(int i);  // the initial value of the 
                                             // i-th variable
  SgExpression *completeInitialValue(int i); // The complete ASSGN_OP
				// expression of the initial value *BW* from M. Golden
  void setInitialValue(int i, SgExpression &initVal;); // sets the initial 
                                // value ofthe i-th variable; this is an
                                // alternative way to initialize variables. 
                                // The low-level node (VAR_REF or ARRAY_REF)
                                // is replaced by a ASSIGN_OP low-level node.
  void clearInitialValue(int i);  // removes initial value of the i-th 
                                  // declaration 
};
```

#### Члены класса
Ниже, varRefValList - это список низкоуровневых узлов с вариантами VAR_REFs, ARRAY_REFs или ASSIGN_OPs.


`**SgVarDeclStmt**`**(SgExpression &varRefValList;, SgExpression &attributeList;, SgType &type;)**

document me

`**SgVarDeclStmt**`**(SgExpression &varRefValList;, SgType &type;)**

document me

`SgType ***type**`**()**

document me

`int **numberOfAttributesF90**`**()**

Этот метод возвращает количество атрибутов F90 (атрибутами F90 являются: PARAMETER_OP, 
PUBLIC_OP, 
PRIVATE_OP, 
ALLOCATABLE_OP, 
EXTERNAL_OP, 
OPTIONAL_OP, 
POINTER_OP 
SAVE_OP TARGET_OP). 
Этот метод назывался numberOfAttributes в версиях Sage++ 1.7 и более ранних. Название было изменено, чтобы избежать конфликтов с методом numberOfAttributes для SgAttributes.

`int **numberOfSymbols**`**()**

document me

`SgSymbol * **symbol**`**(int i)**

document me

`void **deleteSymbol**`**(int i)**

document me

`void **deleteTheSymbol**`**(SgSymbol &symbol;)**

document me

`SgExpression ***initialValue**`**(int i)**

document me

`SgExpression ***completeInitialValue**`**(int i)**

Этот метод возвращает полное выражение ASSGN_OP, содержащее начальное значение для i = 0, 1, 2 ...

`void **setInitialValue**`**(int i, SgExpression &initVal;)**

document me

`void **clearInitialValue**`**(int i)**

Удаляет начальное значение i-го объявления, для i = 0, 1, 2, ...

ПРИМЕЧАНИЕ: В классе [[SgSymbol]] есть несколько методов, которые могут быть очень полезны для создания SgVarDeclStmt при наличии символа.

#### Примеры
[[9 Dump Info - doVarDecl]]
