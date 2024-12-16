Представляет ссылки на константы Fortran, ссылки на типы и ссылки на интерфейсы.

```cpp
class  **SgRefExp**: public SgExpression {
  // Fortran name references
  // variant == CONST_REF, TYPE_REF, INTERFACE_REF
public:
  inline SgRefExp(PTR_LLND ll);
  inline SgRefExp(int variant, SgSymbol &s;);
  inline ~SgRefExp();
};
```

#### Члены класса

`**SgRefExp**`**(PTR_LLND ll)**

document me

`**SgRefExp**`**(int variant, SgSymbol &s;)**

document me
