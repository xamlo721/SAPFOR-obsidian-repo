Представляет аргументы ключевого слова Fortran 90.

```cpp
class **SgKeywordArgExp**: public SgExpression {
  // Fortran 90 keyword argument
  // variant == KEYWORD_ARG
public:
  inline SgKeywordArgExp(PTR_LLND ll);
  inline SgKeywordArgExp(char *argName, SgExpression &exp;);
  inline ~SgKeywordArgExp();
  inline SgSymbol *arg();
  inline SgExpression *value();
};
```

#### Члены класса

`**SgKeywordArgExp**`**(PTR_LLND ll)**

document me

`**SgKeywordArgExp**`**(char *argName, SgExpression &exp;)**

document me

`SgSymbol ***arg**`**()**

document me

`SgExpression ***value**`**()**

document me