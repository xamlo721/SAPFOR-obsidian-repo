Представляет конструкторы массивов Fortran 90.

```cpp
class **SgConstExp**:  public SgExpression {
public:
  inline SgConstExp(PTR_LLND ll);
  inline SgConstExp(SgExpression &values;);
  inline ~SgConstExp();
  inline int numberOfArgs();
  inline SgExpression *arg(int i);
};
```

#### Члены класса

`**SgConstExp**`**(PTR_LLND ll)**

document me

`**SgConstExp**`**(SgExpression &values;)**

document me

`int **numberOfArgs**`**()**

document me

`SgExpression ***arg**`**(int i)**

document me
