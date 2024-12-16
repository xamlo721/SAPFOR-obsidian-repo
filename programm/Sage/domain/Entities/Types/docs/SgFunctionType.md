Представляет типы функций для всех языков. Важной информацией здесь является тип возвращаемого значения.

```cpp
class **SgFunctionType**: public SgType {
  // Function Types have a returned value type
  // variant == T_FUNCTION
public:
  SgFunctionType(SgType &return;_val_type);
  SgType *returnedValue();
  void changeReturnedValue(SgType &rv;);
  ~SgFunctionType();
};
```

#### Члены класса

`**SgFunctionType**`**(SgType &return;_val_type)**

document me

`SgType &**returnedValue**`**()**

document me

`void **changeReturnedValue**`**(SgType &rv;)**

Позволяет изменять возвращаемое значение.
