Представляет собой символы label в C.
```cpp
class **SgLabelSymb**: public SgSymbol {
  // a C label name
  // variant == LABEL_NAME
public:
  inline SgLabelSymb(char *name);
  inline SgLabelSymb(char *name, SgStatement &scope;);
  inline ~SgLabelSymb();
};
```
#### Члены класса

`**SgLabelSymb**`**(char *name)**

document me

