Похоже, что этот класс в настоящее время ни для чего не используется.
```cpp
class **SgDerivedClassType**: public SgType {
  // for example:  typedef int integer;  go to the symbol table
  // for the base type and Id.
  // variant == T_DERIVED_TYPE
public:
  inline SgDerivedType(SgSymbol &type;_name);
  inline SgSymbol * typeName();
  inline ~SgDerivedType();
};
```
#### Члены класса

`**SgDerivedClassType**`**(SgSymbol &type;_name)**

document me

`SgSymbol ***typeName**`**()**

document me