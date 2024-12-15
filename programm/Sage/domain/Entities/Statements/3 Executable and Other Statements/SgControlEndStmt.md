Представляет конечные операторы базовых блоков для всех языков.

```cpp
class  **SgControlEndStmt**: public SgExecutableStatement {
  // the end of a basic block
  // variant == CONTROL_END 
public:
  inline SgControlEndStmt(int variant);
  inline SgControlEndStmt();
  inline ~SgControlEndStmt();
};
```

ПРИМЕЧАНИЕ: В C++ SgControlEnd обычно соответствует }, но его использование непоследовательно, поэтому не следует рассчитывать на то, что SgControlEnd будет отображаться везде, где в коде появляется }. Аналогично, SgControlEnd может появляться в определенных местах, где это не ожидается. Кроме того, вы должны знать, что SgControlEnd также используется для представления пустого определения класса, как в: class A{};. Это было сделано, чтобы отличать такие определения от прямых объявлений, как в class A;.

#### Члены класса

`**SgControlEndStmt**`**(int variant)**

document me

`**SgControlEndStmt**`**()**

document me

#### Примеры
[[5 Expand Syntax - ReplaceWithGetElemPart]]
