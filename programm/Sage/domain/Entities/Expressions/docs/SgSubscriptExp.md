Представляет расширенные ссылки на массивы C и Fortran 90 в виде low:up:stride
```cpp
class **SgSubscriptExp**: public SgExpression {
  // Fortran 90 vector subscript expression
  // variant == DDOT
public:
  inline SgSubscriptExp(PTR_LLND ll);
  inline SgSubscriptExp(SgExpression &lbound;, SgExpression &ubound;, 
                        SgExpression &step;);
  inline SgSubscriptExp(SgExpression &lbound;, SgExpression &ubound;);
  inline ~SgSubscriptExp();
  // perhaps this function can use LlndMapping
  SgExpression *lbound();
  SgExpression *ubound();
  SgExpression *step();
};
```

#### Члены класса

`**SgSubscriptExp**`**(PTR_LLND ll)**

document me

`**SgSubscriptExp**`**(SgExpression &lbound;, SgExpression &ubound;, SgExpression &step;)**

document me

`**SgSubscriptExp**`**(SgExpression &lbound;, SgExpression &ubound;)**

document me

`SgExpression ***lbound**`**()**

document me

`SgExpression ***ubound**`**()**

document me

`SgExpression ***step**`**()**

document me

#### Использование
Чтобы создать ссылку на fortran 90 массив fortran X(1:100:3, i+3) или  "extended" C ссылку на массив X \[1:100:3\]\[i+3]\, мы можем написать
```cpp
     SgVariableSymb xsymb("X"), isymb("i");
     SgVarRefExp  i(isymb);
     SgValueExp  three(3), one(1), hunderd(100);
     SgSubscriptExp range(one, hundred, three);
     SgArrayRefExp(xsymb, range, i+three.copy());
```



