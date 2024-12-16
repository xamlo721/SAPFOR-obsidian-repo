Представляет унарные выражения для всех языков. Существует набор функций, не являющихся членами, которые можно использовать для создания экземпляров класса SgUnaryExp, соответствующих различным вариантам. Описание этих функций приведено в главе "Функции, не являющиеся членами", раздел "Унарные функции".

```cpp
class  **SgUnaryExp**: public  SgExpression {
public:
  inline SgUnaryExp(PTR_LLND ll);
  inline SgUnaryExp(int variant, SgExpression & e);
  inline SgUnaryExp(int variant, int post, SgExpression & e);
  inline int post();
  SgExpression &operand;();
};
```
#### Члены класса

`**SgUnaryExp**`**(PTR_LLND ll)**

document me

`**SgUnaryExp**`**(int variant, SgExpression & e)**

document me

`**SgUnaryExp**`**(int variant, int post, SgExpression & e)**

document me

`int **post**`**()**

document me

`SgExpression &**operand**`**()**

document me

