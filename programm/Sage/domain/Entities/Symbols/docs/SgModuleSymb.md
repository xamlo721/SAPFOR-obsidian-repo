Представляет символы Фортрана для инструкций модуля.
```cpp
class **SgModuleSymb**: public SgSymbol {
  // for fortran module statement
  // variant == MODULE_NAME
public:
  inline SgModuleSymb(char *name);
  inline ~SgModuleSymb();
};
```

#### Члены класса

`**SgModuleSymb**`**(char *name)**

document me

#### Примеры
[[14 Dump Info - classifySymbols]]

