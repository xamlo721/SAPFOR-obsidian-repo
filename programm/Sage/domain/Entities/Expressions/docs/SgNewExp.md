Представляет собой оператор C++ new.
```cpp
class **SgNewExp**: public SgExpression {
// new typename
// new typename (expr)
// variant == NEW_OP
public:
  inline SgNewExp(PTR_LLND ll);
  inline SgNewExp(SgType &t;);
  inline SgNewExp(SgType &t;, SgExpression &e;);
  ~SgNewExp();
};
```

#### Члены класса
`**SgNewExp**`**(PTR_LLND ll)**

document me

`**SgNewExp**`**(SgType &t;)**

document me

`**SgNewExp**`**(SgType &t;, SgExpression &e;)**

document me

`SgExpression &**numberOfArgs**`**()**

document me

`SgExpression &**argument**`**(int i)**

document me
