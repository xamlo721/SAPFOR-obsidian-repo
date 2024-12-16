SgType является базовым классом для всех классов, представляющих типы. Как и в случае с символами, типы в файле формируют список, к которому можно получить доступ с помощью функции SgFile::firstType(). Функция next() возвращает узел типа, следующий за этим. Функция copy() возвращает копию типа node. Многие типы определены в терминах других типов. Например, тип массива имеет базовый тип, который может быть типом указателя, который имеет базовый тип, который может быть целым числом или классом, и т.д. Функция BaseType() всегда обращается к следующему типу в цепочке. Для языка pC++ существует фиктивный тип ElementType, который используется в качестве \"заполнителя\" или параметра для типа, который будет указан позже. Другая функция equivalentToType() может использоваться для проверки типов на эквивалентность. Пожалуйста, смотрите раздел Создание объявлений переменных и параметров для получения дополнительной информации о типах в Sage++.

```cpp
class **SgType** {
public:
  PTR_TYPE thetype;
  SgType(int variant);
  SgType(int var, SgExpression *len,SgType *base);
  SgType(int var, SgSymbol *symb);
  SgType(int var, SgSymbol *firstfield, SgStatement *structstmt);
  inline SgType(PTR_TYPE type);
  inline SgType(SgType &);
  inline int variant();
  inline int id();
  inline SgSymbol *symbol();
  inline SgType &copy();
  inline SgType *copyPtr();
  inline SgType *next();
  inline int isTheElementType();
  inline int equivalentToType(SgType &type;);
  inline int equivalentToType(SgType *type);
  inline SgType *internalBaseType();
  inline int hasBaseType();
  inline SgType *baseType();
  inline SgExpression *length();

/* This code by Andrew Mauer (ajm) */
/*
  maskDescriptors:

  This routine strips many descriptive type traits which you are probably
  not interested in cloning for variable declarations, etc.

  Returns the getTrueType of the base type being described IF there
  are no descriptors which are not masked out. The following masks
  can be specified as an optional second argument:
        MASK_NO_DESCRIPTORS: Do not mask out anything.
        MASK_MOST_DESCRIPTORS: Only leave in: signed, unsigned, short, long,
	                                      const, volatile.
	MASK_ALL_DESCRIPTORS: Mask out everything. 

  If you build your own mask, you should make sure that the traits
  you want to set out have their bits UN-set, and the rest should have
  their bits set. The complementation (~) operator is a good one to use.

  See libSage++.h, where the MASK_*_DESCRIPTORS variables are defined.
*/

   SgType *maskDescriptors (int mask);

/* This code by Andrew Mauer (ajm) */
/*
  getTrueType:

  Since Sage stores dereferenced pointers as PTR(-1) -> PTR(1) -> BASE_TYPE,
  we may need to follow the chain of dereferencing to find the type
  which we expect.

  This code currently assumes that:
  o If you follow the dereferencing pointer (PTR(-1)), you find another
  pointer type or an array type. 

  We do NOT assume that the following situation cannot occur:
      PTR(-1) -> PTR(-1) -> PTR(1) -> PTR(1) -> PTR(-1) -> PTR(1)

  This means there may be more pointers to follow after we come to
  an initial "equilibrium".

  ALGORITHM:

  T_POINTER:
     [WARNING: No consideration is given to pointers with attributes
     (ls_flags) set. For instance, a const pointer is treated the same
     as any other pointer.]
     
     1. Return the same type we got if it is not a pointer type or
     the pointer is not a dereferencing pointer type.

     2. Repeat { get next pointer , add its indirection to current total }
     until the current total is 0. We have reached an equilibrium, so
     the next type will not necessarily be a pointer type.

     3. Check the next type for further indirection with another call
     to getTrueType.

  T_DESCRIPT:
     Returns the result of maskDescriptors called with the given type and mask.

  T_ARRAY:
     If the array has zero dimensions, we pass over it. This type arose
     for me in the following situation:
          double x[2];
	  x[1] = 0;
     
  T_DERIVED_TYPE:
     If we have been told to follow typedefs, get the type of the
     symbol from which this type is derived from, and continue digging.
     Otherwise return this type.

  HITCHES:
     Some programs may dereference a T_ARRAY as a pointer, so we need
     to be prepared to deal with that.
  */

  SgType *getTrueType (int mask = MASK_MOST_DESCRIPTORS, 
                       int follow_typedefs = 0);

  int numberOfAttributes();
  int numberOfAttributes(int type); // of a specified type;
  void *attributeValue(int i); 
  int  attributeType(int i); 
  void *attributeValue(int i,int type); // only considering one type attribute
  void *deleteAttribute(int i); 
  void addAttribute(int type, void *a, int size); // void * can be NULL;
  void addAttribute(int type); //void * is NULL;
  void addAttribute(void *a, int size); //no type specifed;
  void addAttribute(SgAttribute *att);
  SgAttribute *getAttribute(int i);
  SgAttribute *getAttribute(int i,int type);
};
```

#### Члены класса

`**SgType**`**(int variant)**

document me

`**SgType**`**(PTR_TYPE type)**

document me

`int **variant**`**()**

document me

`int **id**`**()**

document me

`SgSymbol ***symbol**`**()**

document me

`SgType &**copy**`**()**

document me

`SgType ***next**`**()**

document me

`int **isTheElementType**`**()**

document me

`int **equivalentToType**`**(SgType &type;)**

document me

`SgType ***internalBaseType**`**()**

document me

`int **hasBaseType**`**()**

document me

`SgType ***baseType**`**()**

document me

`SgType ***getTrueType**` **(int mask = MASK_MOST_DESCRIPTORS, int follow_typedefs = 0)**

Метод описан непосредственно в коде (см. выше). Обратите внимание, что этот метод был написан на C, а не на C++, и может не обрабатывать некоторые типы C++, которых нет в C.


#### Использование

Чтобы проиллюстрировать использование таблицы типов, рассмотрим простую задачу определения того, относится ли переменная в выражении ссылки на переменную к определяемому пользователем классу. Более конкретно, учитывая
```cpp
class myClass;
myClass x, y;
y = x + 2;
```
тогда, если e - это выражение, представляющее переменную, ссылающуюся на x, нам нужна функция isVarRefOfClass (т.е. "MyClass"), которая вернет значение 1, потому что тип класса совпадает. Для этого мы сначала проверяем, действительно ли e является ссылкой на переменную. Затем, извлекая тип символа, мы должны найти производный тип. Из производного типа мы можем найти название класса.

```cpp
int  isVarRefOfClass(SgExpression *e, char *classname){
   SgSymbol *s;
   SgDerivedType *d;
   SgClassSymb *cl;
   SgVarRefExp *exp;
   if((exp = isSgVarRefExp(e)) == NULL) return 0;
   s = exp->symbol();
   if((d = isSgDerivedType(s->type())) == NULL) return 0;
   if(cl = isSgClassSymb(d->typeName()))
         if(!strcmp(cl->identifier(), classname))
                return 1;
   return 0;
}
```
Функция типа
```cpp
SgSUBCLASS * isSgSUBCLASS( SgBASECLASS *)
```
он предусмотрен для каждого подкласса [[SgStatement]], [[SgExpression]] и SgType. Мы считаем, что этот механизм является эффективным способом использования строгой типизации в C++ для уменьшения количества ошибок.

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[1 Instrument - Fortran Program Transformations]]
[[15 Instrument - isReferenceToClassOfElement]]
[[18 Instrument - isReferenceToCollection]]
[[20 Instrument - ListCollectionInstances]]
[[2 Expand Syntax - isArrayRefOfCollection]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[6 Expand Syntax - MatchingDummyVar]]
[[7 Expand Syntax - InDummyVarTable]]
[[8 Expand Syntax - Init]]
[[3 Dump Info - classifyStatements]]
[[12 Dump Info - doFullType]]

