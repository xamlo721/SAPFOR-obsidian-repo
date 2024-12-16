Представляет символы Fortran для внешних функций.

```cpp
class **SgExternalSymb**: public SgSymbol {
  // for fortran external statement
  // variant == ROUTINE_NAME
public:
  inline SgExternalSymb(char *name, SgStatement &scope;);
  inline ~SgExternalSymb();
};
```

#### Члены класса
`**SgExternalSymb**`**(char *name, SgStatement &scope;)**

document me

#### Примеры
[[14 Dump Info - classifySymbols]]
