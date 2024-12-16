Представляет следующие типы:

- C : `struct`, `union`, `enum`
- C++ : `class`
- pC++ : `collection`
- Fortran : `record`
Этот тип очень прост. Он содержит стандартную информацию о типе из [[SgType]], указатель на инструкцию объявления класса и указатель на символ, который является первым полем в структуре. 

Примечание: производные классы имеют другой тип.

```cpp
class **SgClassType**: public SgType {
  // a C struct or Fortran Record, a C++ class, a C Union and a 
  // (note:  C Enum no enums!)
  // and a pC++ collection.  note: derived classes are another type.
  // this type is very simple.  it only contains the standard type
  // info from SgType and a pointer to the class declaration stmt
  // and a pointer to the symbol that is the first field in the struct.
  // variant == T_STRUCT, /*T_ENUM,*/ T_CLASS, T_UNION, T_COLLECTION
public:
  // why is struct_decl needed. No appropriate field found.
  // assumes that first_field has been declared as
  // FIELD_NAME and the remaining fields have been stringed to it.
/*
  SgClassType(int variant, char *name, SgStatement &struct;_decl, int num_fields,
              SgSymbol &first;_field);  //this constructor not implemented BW
*/
  SgClassType(int variant, SgStatement &struct;_decl, SgSymbol &first;_field);
  SgClassType(int variant, SgStatement &struct;_decl);
  inline SgStatement *structureDecl();
  inline SgSymbol *firstFieldSymb();
  SgSymbol *fieldSymb(int i);   //i = 0,1,2, ...
  inline ~SgClassType();
  int numberOfFields();
};
```

#### Члены класса

`**SgClassType**`**(int variant, char *name, SgStatement &struct;_decl, int num_fields, SgSymbol &first;_field)**

document me

`SgStatement ***structureDecl**`**()**

Возвращает указатель на исходный код, который определяет эту структуру.

`SgSymbol ***firstFieldSymb**`**()**

Возвращает указатель на запись символа для первого поля. Символы для всех остальных полей привязаны к этому символу.

`SgSymbol ***fieldSymb**`**(int i)**

Возвращает указатель на i-е поле.

`int **numberOfFields**`**()**

Возвращает количество участников. Полезную информацию смотрите в описании метода SgSymbol \* field(int i).