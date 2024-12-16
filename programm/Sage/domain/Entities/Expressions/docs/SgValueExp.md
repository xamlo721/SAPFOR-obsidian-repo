Представляет собой литералы для всех языков.

```cpp
class  **SgValueExp**: public SgExpression { 
  // a value of one of the base types

  // integers: INT_VAL
  // characters: CHAR_VAL
  // floating point numbers: FLOAT_VAL
  // double precision floating point numbers: DOUBLE_VAL
  // strings: STRING_VAL
  // complex numbers: COMPLEX_VAL 
  // long double numbers: LONG_DOUBLE_VAL
  // long integers:  LONG_INT_VAL
  // unsigned integers: UNSIGNED_INT_VAL
  // unsigned long integers: UNSIGNED_LONG_INT_VAL

public:
  inline SgValueExp(int value);
  SgValueExp(unsigned int val);  // makes 10u, for example
  SgValueExp(long int val);      // makes 10l, for example
  SgValueExp(long unsigned int val); //makes 10ul, for example
  inline SgValueExp(char char_val);
  inline SgValueExp(float float_val);   // makes 10.0f, for example
  inline SgValueExp(double double_val); // makes 10.0, for example
  inline SgValueExp(char *string_val);
  SgValueExp(long double val);   // makes 10.0l, for example
  SgValueExp(int variant, char *value_string); 
              // variant = FLOAT_VAL, DOUBLE_VAL, LONG_DOUBLE_VAL 
  inline SgValueExp(double real, double imaginary);
  inline SgValueExp(SgValueExp ℜ, SgValueExp &imaginary;);
  inline void setValue(int int_val);
  inline void setValue(char char_val);
  inline void setValue(float float_val);
  inline void setValue(double double_val);
  inline void setValue(char *string_val);
  inline void setValue(double real, double im);
  inline void setValue(SgValueExp ℜ, SgValueExp & im);
  inline int intValue();
  inline char*  floatValue();
  inline char  charValue();
  inline char*  doubleValue();
  inline char * stringValue();
  inline SgExpression *realValue();
  inline SgExpression *imaginaryValue();
};
```
#### Члены класса

`inline **SgValueExp**`**(int value)**

document me

`**SgValueExp**`**(unsigned int value)**

makes 10u, for example

`**SgValueExp**`**(long int value)**

makes 10l, for example

`**SgValueExp**`**(long unsigned int value)**

makes 10ul, for example

`inline **SgValueExp**`**(char char_val)**

document me

`inline **SgValueExp**`**(float float_val)**

document me

`inline **SgValueExp**`**(double double_val)**

document me

`inline **SgValueExp**`**(char *string_val)**

document me

`**SgValueExp**`**(long double val)**

document me

`**SgValueExp**`**(int variant, char *value_string)**

Note: variant = `**FLOAT_VAL**`, `**DOUBLE_VAL**`, and `**LONG_DOUBLE_VAL**`.

`inline **SgValueExp**`**(double real, double imaginary)**

document me

`inline **SgValueExp**`**(SgValueExp ℜ, SgValueExp &imaginary;)**

document me

`inline void **setValue**`**(int int_val)**

document me

`inline void **setValue**`**(char char_val)**

document me

`inline void **setValue**`**(float float_val)**

document me

`inline void **setValue**`**(double double_val)**

document me

`inline void **setValue**`**(char *string_val)**

document me

`inline void **setValue**`**(double real, double im)**

document me

`inline void **setValue**`**(SgValueExp ℜ, SgValueExp & im)**

document me

`inline int **intValue**`**()**

document me

`inline char ***floatValue**`**()**

document me

`inline char **charValue**`**()**

document me

`inline char ***doubleValue**`**()**

document me

`inline char ***stringValue**`**()**

document me

`inline SgExpression ***realValue**`**()**

document me

`inline SgExpression ***imaginaryValue**`**()**

document me

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[4 Instrument - InsertFCallNode]]
[[3 Dump Info - classifyStatements]]
