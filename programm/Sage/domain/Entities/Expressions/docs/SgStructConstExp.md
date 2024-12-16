Представляет структурные конструкторы Fortran 90.
```cpp
class **SgStructConstExp**:  public SgExpression {
  // Fortran 90 structure constructor
  // variant == STRUCTURE_CONSTRUCTOR
public:
  inline SgStructConstExp(PTR_LLND ll);
  // further checks on values need to be done.
  inline SgStructConstExp(SgSymbol &structName;, SgExpression &values;);
  inline SgStructConstExp(SgExpression  &typeRef;, SgExpression &values;);
  inline ~SgStructConstExp();
  inline int numberOfArgs();
  inline SgExpression *arg(int i);
};
```

#### Члены класса

`**SgStructConstExp**`**(PTR_LLND ll)**

document me

`**SgStructConstExp**`**(SgSymbol &structName;, SgExpression &values;)**

document me

`**SgStructConstExp**`**(SgExpression &typeRef;, SgExpression &values;)**

document me

`int **numberOfArgs**`**()**

document me

`SgExpression ***arg**`**(int i)**

document me





