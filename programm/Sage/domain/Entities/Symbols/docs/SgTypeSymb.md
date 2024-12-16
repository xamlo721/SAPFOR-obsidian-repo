Представляет символы C typedef.
```cpp
class **SgTypeSymb**: public SgSymbol {
  // a C typedef.  the type() function returns the base type.
  // variant == TYPE_NAME
public:
  SgTypeSymb(char *name, SgType &baseType;);
  SgType &baseType;();
  ~SgTypeSymb();
};
```

#### Члены класса

`**SgTypeSymb**`**(char *name, SgType &baseType;)**

document me

Тип, который представляет этот символ.
`SgType &**baseType**`**()**

