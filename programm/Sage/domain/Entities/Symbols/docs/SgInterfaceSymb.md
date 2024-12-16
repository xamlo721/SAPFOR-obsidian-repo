Представляет символы Fortran 90 для инструкций интерфейса модуля.

```cpp
class **SgInterfaceSymb**: public SgSymbol {
  // for fortran interface statement
  // variant == INTERFACE_NAME
public:
  inline SgInterfaceSymb(char *name, SgStatement &scope;);
  inline ~SgInterfaceSymb();
};
```

#### Члены класса
`**SgInterfaceSymb**`**(char *name, SgStatement &scope;)**

document me

#### Примеры
[[14 Dump Info - classifySymbols]]
