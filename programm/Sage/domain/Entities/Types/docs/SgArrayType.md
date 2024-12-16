Представляет типы массивов для всех языков. Синтаксический анализатор присваивает каждой переменной массива свой собственный объект-дескриптор типа массива.

```cpp
class **SgArrayType**: public SgType {
  // A new array type is generated for each array.
  // variant == T_ARRAY
public:
  inline SgArrayType(SgType &base;_type);
  inline int dimension();
  inline SgExpression *sizeInDim(int i);
  inline void addDimension(SgExpression *e);
  inline SgExpression * getDimList();
  inline SgType * baseType();
  inline void setBaseType(SgType &bt;);
  inline void addRange(SgExpression &e;);
  inline ~SgArrayType();
};
```
#### Члены класса

`**SgArrayType**`**(SgType &base;_type)**

Каждый массив должен иметь базовый тип, который может быть объектом любого типа.

`int **dimension**`**()**

document me

`SgExpression ***sizeInDim**`**(int i)**

Возвращает выражение, описывающее форму массива. Если это выражение является [[SgSubscriptExp]], то это массив Fortran, который имеет не единичный начальный индекс и индекс верхней границы.

`SgType ***baseType**`**()**

document me

`void **setBaseType**`**(SgType &bt;)**

Modifies the base type.

`void **addRange**`**(SgExpression &e;)**

Позволяет добавить новое измерение.

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[12 Dump Info - doFullType]]
