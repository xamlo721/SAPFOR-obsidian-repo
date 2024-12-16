Представляет экземпляры, связанные с индексной переменной Fortran, и представление диапазона выполнения цикла.
```cpp
class **SgIOAccessExp**: public SgExpression {
  // Fortran index variable bound instantiation
  // variant == IOACCESS
  //used for do-loop range representation also.
  // this form needs to be standardized. 
public:
  inline SgIOAccessExp(PTR_LLND ll);
  // type-checking on bounds needs to be done.
  // Float values are legal in some cases. check manual.
  inline SgIOAccessExp(SgSymbol &s;, SgExpression lbound, 
                       SgExpression ubound, SgExpression step);
  inline SgIOAccessExp(SgSymbol &s;, SgExpression lbound, 
                       SgExpression ubound);
  inline ~SgIOAccessExp();
};
```
#### Члены класса

`**SgIOAccessExp**`**(PTR_LLND ll)**

document me

`**SgIOAccessExp**`**(SgSymbol &s;, SgExpression lbound, SgExpression ubound, SgExpression step)**

document me

`**SgIOAccessExp**`**(SgSymbol &s;, SgExpression lbound, SgExpression ubound)**

document me