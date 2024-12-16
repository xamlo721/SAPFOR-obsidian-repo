Представляет управляющие аргументы Fortran по умолчанию для операторов ввода-вывода.
```cpp
class **SgSpecPairExp**: public SgExpression {
  // Fortran default control arguments to Input/Output statements
  // variant == SPEC_PAIR
public:
  inline SgSpecPairExp(PTR_LLND ll);
  inline SgSpecPairExp(SgExpression &arg;, SgExpression &value;);
  inline SgSpecPairExp(SgExpression &arg;);
  inline SgSpecPairExp(char *arg, char *value);
  inline ~SgSpecPairExp();
  inline SgExpression *arg();
  inline SgExpression *value();
};
```
#### Члены класса

`**SgSpecPairExp**`**(PTR_LLND ll)**

document me

`**SgSpecPairExp**`**(SgExpression &arg;, SgExpression &value;)**

document me

`**SgSpecPairExp**`**(SgExpression &arg;)**

document me

`**SgSpecPairExp**`**(char *arg, char *value)**

document me

`SgExpression ***arg**`**()**

document me

`SgExpression ***value**`**()**

document me
