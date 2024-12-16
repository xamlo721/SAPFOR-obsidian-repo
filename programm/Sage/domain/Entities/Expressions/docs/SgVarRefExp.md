Представляет ссылки на скалярные переменные и неиндексированные массивы для всех языков.
```cpp
class  **SgVarRefExp**: public SgExpression {
  // scalar variable reference or non-indexed array reference
  // variant == VAR_REF
public:
  inline SgVarRefExp (PTR_LLND ll);
  inline SgVarRefExp(SgSymbol &s;);
  inline SgVarRefExp(SgSymbol *s);
  SgExpression *progatedValue(); // if scalar propogation worked
  inline ~SgVarRefExp();
};
```
#### Члены класса
`**SgVarRefExp**`**(PTR_LLND ll)**

document me

`**SgVarRefExp**`**(SgSymbol &s;)**

document me

`**SgVarRefExp**`**(SgSymbol *s)**

document me

`SgExpression ***progatedValue**`**()**

document me

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[14 Instrument - isReferenceToMethodOfElement]]
[[15 Instrument - isReferenceToClassOfElement]]
[[18 Instrument - isReferenceToCollection]]
[[1 Expand Syntax - isReferenceToElementField]]
[[2 Expand Syntax - isArrayRefOfCollection]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[8 Expand Syntax - Init]]

















