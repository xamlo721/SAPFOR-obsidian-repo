Представляет коллекции pC++.
```cpp
class **SgCollectionStmt**: public SgClassStmt {
  // basic C++ structure
  // collection name ;
  //                    body
  //                } variables_list;
  // variant == COLLECTION_DECL
public:
  inline SgCollectionStmt();
  inline SgCollectionStmt(SgSymbol &name;);
  inline ~SgCollectionStmt();
  inline SgStatement *firstElementMethod();
};
```
#### Члены Класса 

document me
`**SgCollectionStmt**`**()**


document me
`**SgCollectionStmt**`**(SgSymbol &name;)**


document me
`SgStatement ***firstElementMethod**`**()**

#### Использование


#### Примеры
[[19 Instrument - ListCollections]]