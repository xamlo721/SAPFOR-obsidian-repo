Представляет вызовы функций для всех языков.
```cpp
Represents function calls, for all languages.

class **SgFunctionCallExp**: public {SgExpression} {
  // function_name(expr1, expr2, ....)
  // variant == FUNC_CALL
public:
  inline SgFunctionCallExp(PTR_LLND ll);
  inline SgFunctionCallExp(SgSymbol &fun;, SgExpression ¶mList;);
  inline SgFunctionCallExp(SgSymbol &fun;);
  inline ~SgFunctionCallExp();
  inline SgSymbol *funName();
  inline SgExpression *args();
  inline int numberOfArgs();
  inline SgExpression *arg(int i);
  inline void addArg(SgExpression &arg;);
};
```

#### Члены класса

`inline **SgFunctionCallExp**`**(PTR_LLND ll)**

document me

`inline **SgFunctionCallExp**`**(SgSymbol &fun;, SgExpression ¶mList;)**

document me

`inline **SgFunctionCallExp**`**(SgSymbol &fun;)**

document me

`SgSymbol ***funName**`**()**

document me

`SgExpression ***args**`**()**

document me

`int **numberOfArgs**`**()**

document me

`SgExpression ***arg**`**(int i)**

document me

`void **addArg**`**(SgExpression &arg;)**

document me

#### Примеры
[[14 Instrument - isReferenceToMethodOfElement]]
[[15 Instrument - isReferenceToClassOfElement]]
[[18 Instrument - isReferenceToCollection]]
[[25 Instrument - InsertCCallNode]]
[[3 Expand Syntax - ExpandSyntax]]
