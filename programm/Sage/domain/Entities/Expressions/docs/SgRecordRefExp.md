Представляет ссылки на поля в структурах на языке Си.
```cpp
class **SgRecordRefExp**: public SgExpression {
  // a field reference of a structure
  // variant == RECORD_REF
public:
  inline SgRecordRefExp(PTR_LLND ll);
  inline SgRecordRefExp(SgSymbol &recordName;, char *fieldName);
  inline SgRecordRefExp(SgExpression &recordExp;, char *fieldName);
  inline ~SgRecordRefExp();
  inline SgSymbol *fieldName();
  inline SgSymbol *recordName();
  inline SgExpression *record();
};
```
#### Члены классов
`**SgRecordRefExp**`**(PTR_LLND ll)**

document me

`**SgRecordRefExp**`**(SgSymbol &recordName;, char *fieldName)**

document me

`**SgRecordRefExp**`**(SgExpression &recordExp;, char *fieldName)**

document me

`SgSymbol ***fieldName**`**()**

document me

`SgSymbol ***recordName**`**()**

document me

`SgExpression ***record**`**()**

document me

#### Примеры




