Представляет символы Фортрана для имен конструкций.

```cpp
class **SgConstructSymb**: public SgSymbol {
  // for fortran statement with construct names
  // variant == CONSTRUCT_NAME
public:
  inline SgConstructSymb(char *name, SgStatement &scope;);
  inline ~SgConstructSymb();
};
```

#### Члены класса

`**SgConstructSymb**`**(char *name, SgStatement &scope;)**

document me

#### Примеры
[[14 Dump Info - classifySymbols]]