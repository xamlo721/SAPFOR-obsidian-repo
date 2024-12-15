Представляет структуры C++.

```cpp
class **SgStructStmt**: public SgClassStmt {

  // basic C++ structure
  // struct name ;
  //                   body
  //              } variables_list;
  // variant == STRUCT_DECL
public:
  // consider like a class.
  inline SgStructStmt();
  inline SgStructStmt(SgSymbol &name;);
  inline ~SgStructStmt();
};
```


#### Члены Класса 
document me
`**SgStructStmt**`**()**


Это подкласс класса SgClassStmt. Вариант здесь - STRUCT_DECL. Остальные функциональные возможности такие же, как и у SgClassStmt.
`**SgStructStmt**`**(SgSymbol &name;)**

#### Использование


#### Примеры
