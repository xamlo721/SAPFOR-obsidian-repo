Представляет символы для констант, для всех языков.
```cpp
class **SgConstantSymb**: public SgSymbol {
  // a symbol for a constant object
  // variant == CONST_NAME 
public:
  inline SgConstantSymb(char *identifier, SgStatement &scope;, 
                 SgExpression &value;);
  inline ~SgConstantSymb();
  inline SgExpression *constantValue();
};
```

#### Члены класса

`**SgConstantSymb**`**(char *identifier, SgStatement &scope;, SgExpression &value;)**

document me

`SgExpression ***constantValue**`**()**

document me
#### Примеры
[[14 Dump Info - classifySymbols]]
