Представляет собой USE выражение Fortran 90.

```cpp
class **SgUseRenameExp**: public SgExpression {
  // Fortran 90 USE statement renaming
  // variant == RENAME_NODE
public:
  inline SgUseRenameExp(PTR_LLND ll);
  inline SgUseRenameExp(SgSymbol &newName;, SgSymbol &oldName;);
  inline ~SgUseRenameExp();
  inline SgSymbol *newName();
  inline SgSymbol *oldName();
  inline SgExpression *newNameExp();
  inline SgExpression *oldNameExp();
};
```

#### Члены класса

`**SgUseRenameExp**`**(PTR_LLND ll)**

document me

`**SgUseRenameExp**`**(SgSymbol &newName;, SgSymbol &oldName;)**

document me

`SgSymbol ***newName**`**()**

document me

`SgSymbol ***oldName**`**()**

document me

`SgExpression ***newNameExp**`**()**

document me

`SgExpression ***oldNameExp**`**()**

document me