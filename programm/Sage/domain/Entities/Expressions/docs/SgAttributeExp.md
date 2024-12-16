Представляет атрибуты Fortran 90.

```cpp
class **SgAttributeExp**: public SgExpression {
  // Fortran 90 attributes
  // variant ==  PARAMETER_OP, PUBLIC_OP, PRIVATE_OP, ALLOCATABLE_OP,
  // DIMENSION_OP, EXTERNAL_OP, IN_OP, OUT_OP, INOUT_OP, INTRINSIC_OP, 
  // POINTER_OP, OPTIONAL_OP, SAVE_OP, TARGET_OP
public:
  inline SgAttributeExp(PTR_LLND ll);
  inline SgAttributeExp(int variant);
  inline ~SgAttributeExp();
};
```

#### Члены класса

`**SgAttributeExp**`**(PTR_LLND ll)**

document me

`**SgAttributeExp**`**(int variant)**

document me

