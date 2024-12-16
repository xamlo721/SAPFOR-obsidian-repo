Представляет символы Fortran для обозначения переменных-меток для назначенных инструкций goto.
```cpp
class **SgLabelVarSymb**: public SgSymbol {
  // a Fortran label variable for an assigned goto stmt
  // variant == LABEL_NAME
public:
  inline SgLabelVarSymb(char *name, SgStatement &scope;);
  inline ~SgLabelVarSymb();
};
```

#### Члены класса

`**SgLabelVarSymb**`**(char *name, SgStatement &scope;)**

document me

#### Примеры
[[14 Dump Info - classifySymbols]]
