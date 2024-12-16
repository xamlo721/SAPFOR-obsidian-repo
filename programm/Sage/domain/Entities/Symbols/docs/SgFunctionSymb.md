Представляет символы для подпрограммы, функции и основной программы для всех языков.

```cpp
class **SgFunctionSymb**: public SgSymbol {
  // a subroutine, function or main program
  // variant == PROGRAM_NAME, PROCEDURE_NAME, or FUNCTION_NAME
public:
  SgFunctionSymb(int variant);
  SgFunctionSymb(int variant, char *identifier, SgType &t;, 
                 SgStatement &scope;);
  ~SgFunctionSymb();
  inline void addParameter(SgSymbol ¶meters;);
  void insertParameter(int position, SgSymbol &symb;);
  int numberOfParameters();
  SgSymbol *parameter(int i); 
  SgSymbol *result();
  void  setResult(SgSymbol &symbol;);
};
```

#### Члены класса

`**SgFunctionSymb**`**(int variant)**

document me

`**SgFunctionSymb**`**(int variant, char *identifier, SgType &t;, SgStatement &scope;)**

document me

`void **addParameter**`**(int n, SgSymbol ¶meters;)**

document me

`void **insertParameter**`**(int position, SgSymbol &symb;)**

document me

`int **numberOfParameters**`**()**

Returns number of parameters in the formal parameter list (of a function).

`SgSymbol ***parameter**`**(int i)**

Returns the `i`th parameter in the formal parameter list (of a function).

`SgSymbol ***result**`**()**

For Fortran, returns a pointer to the result symbol.

`void **setResult**`**(SgSymbol &symbol;)**

For Fortran.

`int **isRecursive**`**()**

For Fortran, returns _True_ if the function is recursive.

`int **setRecursive**`**()**

document me

#### Примеры
[[2 Instrument - InitSymbols]]
[[23 Instrument - CInitSymbols]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[8 Expand Syntax - Init]]
[[14 Dump Info - classifySymbols]]

