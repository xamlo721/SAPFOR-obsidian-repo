Представляет символы языка Си для полей в перечислениях, символы для полей в структурах и символы для полей в классах.

```cpp
class **SgFieldSymb**: public SgSymbol {
  // a field in an enum or in a struct.
  // variant == ENUM_NAME or FIELD_NAME
public:
  // no check is made to see if the field "identifier"
  //   already exists in the structure. 
  inline SgFieldSymb(char *identifier, SgType &t;, SgSymbol &structureName;);
  inline ~SgFieldSymb();
  inline int offset();        // position in the structure
  inline SgSymbol *structureName();  // parent structure
  inline SgSymbol *nextField();
  inline int isMethodOfElement();
};
```

#### Члены класса

`**SgFieldSymb**`**(char *identifier, SgType &t;, SgSymbol &structureName;)**

document me

`int **offset**`**()**

document me

`SgSymbol ***structureName**`**()**

document me

`SgSymbol ***nextField**`**()**

document me

`int **isMethodOfElement**`**()**

document me

`int **isPrivate**`**()**

document me

`int **isSequence**`**()**

document me

`void **setPrivate**`**()**

document me

`void **setSequence**`**()**

document me

#### Примеры
[[14 Instrument - isReferenceToMethodOfElement]]
[[15 Instrument - isReferenceToClassOfElement]]
[[1 Expand Syntax - isReferenceToElementField]]
