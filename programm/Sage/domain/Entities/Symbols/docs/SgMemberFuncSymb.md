Представляет символы языка Си для членов структур и классов.

```cpp
class **SgMemberFuncSymb**: public SgFunctionSymb {
  // a member function for a class or struct or collection
  // variant = MEMBER_FUNC
  // may be either MEMB_PRIVATE, MEMB_PUBLIC,
  // MEMP_METHOELEM or MEMB_PROTECTED
public:
  inline SgMemberFuncSymb(char *identifier, SgType &t;, SgStatement &cla;,
                          int status);
  inline ~SgMemberFuncSymb();
  inline int isMethodOfElement();
  inline SgSymbol *className();
  inline void setClassName(SgSymbol &symb;);
};
```

#### Члены класса

`**SgMemberFuncSymb**`**(char *identifier, SgType &t;, SgStatement &cla;, int status)**

document me

`int **status**`**()**

Возвращает protection status символа.

`int **isVirtual**`**()**

document me

`int **isMethodOfElement**`**()**

document me

`SgSymbol ***className**`**()**

Возвращает запись таблицы символов для заключающего ее класса или структуры.

`void **setClassName**`**(SgSymbol &symb;)**

document me

#### Примеры
[[14 Instrument - isReferenceToMethodOfElement]]
[[15 Instrument - isReferenceToClassOfElement]]
[[16 Instrument - inMethodOfTheElement]]
[[17 Instrument - whichFunctionAmI]]

