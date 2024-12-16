Представляет переменные символы для всех языков.
```cpp
class **SgVariableSymb**: public SgSymbol {
  // a variable
  // variant = VARIABLE_NAME
public:
  inline SgVariableSymb(char *identifier, SgType &t;, SgStatement &scope;);
  inline SgVariableSymb(char *identifier, SgType *t, SgStatement *scope);
  inline SgVariableSymb(char *identifier, SgType &t;);
  inline SgVariableSymb(char *identifier,  SgStatement &scope;);
  inline SgVariableSymb(char *identifier,  SgStatement *scope);
  inline SgVariableSymb(char *identifier);
  inline ~SgVariableSymb();

  /* This function allocates and returns a new variable reference
     expression to this symbol. (ajm) */
  inline SgVarRefExp *varRef (void);
};
```
#### Члены класса

`**SgVariableSymb**`**(char *identifier, SgType &t;, SgStatement &scope;)**

document me

`**SgVariableSymb**`**(char *identifier, SgType &t;)**

document me

`**SgVariableSymb**`**(char *identifier, SgStatement &scope;)**

document me

`**SgVariableSymb**`**(char *identifier)**

document me


#### Примеры
[[2 Restructure - addStuffToProgram]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[8 Expand Syntax - Init]]
[[14 Dump Info - classifySymbols]]
