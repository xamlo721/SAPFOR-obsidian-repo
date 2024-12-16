Этот тип используется для представления типов переменных, которые в C++ определяются пользователем. Они могут быть определены с помощью typedef или class. Например, с помощью объявления:

```cpp
     class A a;
```
типом символа, соответствующего a, является SgDerivedType, имя которого указывает на символ, соответствующий A. Обратите внимание, что типом A является не SgDerivedType, а скорее [[SgClassType]].
```cpp
class **SgDerivedType**: public SgType {
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
`**SgDerivedType**`**(SgSymbol &type;_name)**

document me

`SgSymbol ***typeName**`**()**

Возвращает объект класса SgTypeSymb или SgClassSymb, к которому относится этот тип.

#### Примеры
[[15 Instrument - isReferenceToClassOfElement]]
[[12 Dump Info - doFullType]]
