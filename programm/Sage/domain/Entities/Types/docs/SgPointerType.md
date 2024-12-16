Представляет тип указателя на языке Си. Важная информация закодирована в базовом типе, т.е. в типе объекта, на который может указывать этот указатель.

```cpp
lass **SgPointerType**: public SgType {
  // A pointer type contains only one hany bit of information:
  // the base type.
  // can also have a modifier like BIT_CONST BIT_GLOBAL. see SgDescriptType.
  // variant == T_POINTER
public:
  SgPointerType(SgType &base;_type);
  SgPointerType(SgType *base_type);
  inline SgType *baseType();
  inline int indirection();
  inline void setIndirection(int);
  inline int modifierFlag();
  inline void setModifierFlag(int flag); 
  inline void setBaseType(SgType &baseType;);
  inline ~SgPointerType();
};
```

#### Члены класса

`**SgPointerType**`**(SgType &base;_type)**

document me

`**SgPointerType**`**(SgType *base_type)**

document me

`SgType ***baseType**`**()**

document me

`int **indirection**`**()**

document me

`void **setIndirection**`**(int)**

document me

`inline int **modifierFlag**`**()**

Возвращает спецификацию decl (для таких объектов, как const), которые ссылаются на типы указателей (например, int \*const;)

`inline void **setModifierFlag**`**(int flag)**

Устанавливает decl-спецификации (такие как const), которые ссылаются на типы указателей (например: int * const:)

`void **setBaseType**`**(SgType &baseType;)**

Можно изменить базовый тип.

#### Примеры
[[18 Instrument - isReferenceToCollection]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[8 Expand Syntax - Init]]
[[12 Dump Info - doFullType]]


