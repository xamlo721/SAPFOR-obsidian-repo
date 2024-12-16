Представляет ссылки на метки Fortran.

```cpp
class **SgLabelRefExp**: public SgExpression {
  // Fortran label reference
  // variant == LABEL_REF
public:
  inline SgLabelRefExp(PTR_LLND ll);
  inline SgLabelRefExp(SgLabel &label;);
  inline ~SgLabelRefExp();
  inline SgLabel *label();
};
```

#### Члены класса

`**SgLabelRefExp**`**(PTR_LLND ll)**

document me

`**SgLabelRefExp**`**(SgLabel &label;)**

document me

`SgLabel ***label**`**()**

document me