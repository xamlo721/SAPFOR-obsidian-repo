Представляет ссылочные типы C++.
```cpp
class **SgReferenceType**: public SgType {
  // A reference (&xx; in c+=) type contains only one hany bit of information:
  // the base type.
  // variant == T_REFERENCE
public:
  inline SgReferenceType(SgType &base;_type);
  inline SgType *baseType();
  inline void setBaseType(SgType &baseType;);
  inline ~SgReferenceType();
  inline int modifierFlag();
  inline void setModifierFlag(int flag); 
};
```
#### Члены класса
`**SgReferenceType**`**(SgType &base;_type)**

document me

`SgType ***baseType**`**()**

document me

`void **setBaseType**`**(SgType &baseType;)**

document me

#### Примеры
[[18 Instrument - isReferenceToCollection]]
[[12 Dump Info - doFullType]]

