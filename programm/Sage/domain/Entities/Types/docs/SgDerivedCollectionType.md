Представляет классы коллекции pC++.

```cpp
class **SgDerivedCollectionType**: public SgType {
  // for example:
  // Collection DistributedArray {body1} ;
  // class object {body2} ;
  // DistributedArray<object>  X;
  // X is of type with variant = T_DERIVED_COLLECTION
public:
  inline SgDerivedCollectionType(SgSymbol &s;, SgType &t;);
  inline SgType *elementClass();
  inline void setElementClass(SgType &ty;);
  inline SgSymbol *collectionName();
  inline SgStatement *createCollectionWithElemType();
  inline ~SgDerivedCollectionType();
};
```

#### Члены класса

`**SgDerivedCollectionType**`**(SgSymbol &s;, SgType &t;)**

t - это тип коллекции.

`SgType ***elementClass**`**()**

Возвращает тип элемента коллекции.

`void **setElementClass**`**(SgType &ty;)**

Задает тип элемента коллекции.

`SgSymbol ***collectionName**`**()**

Возвращает объект класса SgClassSymb, который является именем коллекции.

`SgStatement ***createCollectionWithElemType**`**()**

document me

#### Примеры
[[15 Instrument - isReferenceToClassOfElement]]
[[18 Instrument - isReferenceToCollection]]
[[20 Instrument - ListCollectionInstances]]
[[21 Instrument - ListCollectionInvocations]]
[[26 Instrument - CTimingInstrumentSub]]
[[2 Expand Syntax - isArrayRefOfCollection]]
[[4 Expand Syntax - SearchInExpForCollectionArrayRef]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[8 Expand Syntax - Init]]
[[12 Dump Info - doFullType]]


