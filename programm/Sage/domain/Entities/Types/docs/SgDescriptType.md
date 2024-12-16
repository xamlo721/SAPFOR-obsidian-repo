Представляет следующие типы:

- C : `unsigned`, `signed`, `long`, `short`, `extern`, `static`, `register`
- C++ : `private`, `virtual`, `inline`, `volatile`, `const`, `auto`, `friend`
- Fortran 90 : `syn`, `shared`, `future`, `global`

Этот класс представляет объекты-дескрипторы, которые изменяют объекты других типов. До версии 1.7 спецификации friend, extern, static и inline decl обрабатывались с использованием SgDescriptType. Начиная с версии 1.9, они являются модификаторами узлов  [[SgStatement]] (дополнительную информацию смотрите в разделе, посвященном SgStatement).

```cpp
class **SgDescriptType**: public SgType {
  // for example in C: long volatile int x; 
  // long and volatile are modifiers and there is a descriptor
  // type whose base type is the real type of x.
  // the modifier is an integer with bits set if the modifier
  // holds.
  // the bits are:
  // BIT_SYN, BIT_SHARED, BIT_PRIVATE, BIT_FUTURE, BIT_VIRTUAL, 

  // BIT_UNSIGNED, BIT_SIGNED, BIT_LONG, BIT_SHORT,
  // BIT_VOLATILE, BIT_CONST, BIT_TYPEDEF, BIT_AUTO,
  // BIT_REGISTER, BIT_GLOBAL, and more.
  //
  // variant = T_DESCRIPT
public:
  inline SgDescriptType(SgType &base;_type, int bit_flag);
  inline int modifierFlag();
  inline void setModifierFlag(int flag);
  inline ~SgDescriptType();
};
```

#### Члены класса

`**SgDescriptType**`**(SgType &base;_type, int bit_flag)**

document me

`int **modifierFlag**`**()**

document me

`void **setModifierFlag**`**(int flag)**

document me

#### Примеры
[[12 Dump Info - doFullType]]

