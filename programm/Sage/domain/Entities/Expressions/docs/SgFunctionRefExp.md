Представляет ссылки на функции для всех языков.

```cpp
class **SgFunctionRefExp**: public {SgExpression} {
   // function_name(formal args)  - for function headers and protytpes.
   // variant = FUNCTION_REF
public:
  inline SgFunctionRefExp(PTR_LLND ll);
  inline SgFunctionRefExp(SgSymbol &fun;);
  inline ~SgFunctionRefExp();
  inline SgSymbol *funName();
  inline SgExpression *args();
  inline int numberOfArgs();
  inline SgExpression *arg(int i);
  SgExpression * AddArg(char *, SgType &);
}
```
#### Члены класса

`inline **SgFunctionRefExp**`**(PTR_LLND ll)**

document me

`inline **SgFunctionRefExp**`**(SgSymbol &fun;)**

document me

`inline ~**SgFunctionRefExp**`**()**

document me

`inline SgSymbol ***funName**`**()**

document me

`inline SgExpression ***args**`**()**

document me

`inline int **numberOfArgs**`**()**

document me

`inline SgExpression ***arg**`**(int i)**

document me

`SgExpression ***AddArg**`**(char *, SgType &)**

Смотрите раздел "Указатели на функции" для получения подробного описания того, как использовать этот метод.


