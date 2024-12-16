Представляет собой C++ delete.

```cpp
class **SgDeleteExp**: public SgExpression {
// delete [size]  expr
// variant == DELETE_OP
public:
  inline SgDeleteExp(PTR_LLND ll);
  inline SgDeleteExp(SgExpression &size;, SgExpression &expr;);
  inline SgDeleteExp(SgExpression &expr;);
  inline ~SgDeleteExp();
};
```

#### Члены класса
`**SgDeleteExp**`**(PTR_LLND ll)**

document me

`**SgDeleteExp**`**(SgExpression &size;, SgExpression &expr;)**

document me

`**SgDeleteExp**`**(SgExpression &expr;)**

document me