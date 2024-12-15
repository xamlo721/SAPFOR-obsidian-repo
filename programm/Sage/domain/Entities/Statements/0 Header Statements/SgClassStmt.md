Представляет классы C++.

```cpp
class **SgClassStmt**: public {SgStatement} {
  // C++ class statement
  //    class name : superclass_list ElementTypeOf collection_name {
  //            body
  //     } variables_list;
  // variant == CLASS_DECL, IDL_INTERFACE_DECL, IDL_MODULE_DECL,
  //            IDL_EXCEPTION_DECL
public:
  inline SgClassStmt(int variant);
  inline SgClassStmt(SgSymbol &name;);
  inline SgClassStmt(int variant, SgSymbol &name;);
  inline ~SgClassStmt();
  inline int numberOfSuperClasses();
  inline SgSymbol *name();
  SgSymbol *superClass(int i);
  void setSuperClass(int i, SgSymbol &symb;);
  void setSuperClass(int i, SgSymbol &symb;, int access);
                                 //access = one of BIT_PRIVATE
                                 //         BIT_PROTECTED
                                 //         BIT_PUBLIC
                                 //         BIT_PRIVATE | BIT_VIRTUAL
                                 //         BIT_PROTECTED | BIT_VIRTUAL
                                 //         BIT_PUBLIC | BIT_VIRTUAL
};
```
Объявление класса состоит из имени, списка суперклассов, тела, состоящего из общедоступных, частных и защищенных функций и полей, и списка переменных, дающих имена экземплярам, массивам экземпляров, указателям на экземпляры и ссылкам на экземпляры класса.

#### Члены класса

document me
`**SgClassStmt**`**(int variant)**


document me
`**SgClassStmt**`**(SgSymbol &name;)**


document me
`int **numberOfSuperClasses**`**()**


document me
`SgSymbol ***name**`**()**


document me
`SgSymbol ***superClass**`**(int i)**


document me
`void **setSuperClass**`**(int i, SgSymbol &symb;)**

#### Использование
SgClassStmt представляет как прямые объявления классов, как в: 
```cpp
class A;
```
так и реальные объявления классов (то есть определения), как в: 
```cpp
class A { 
	public:
		int field1; 
		int field2;
}; 
```

Объявления вида, 
```cpp
class A a;
``` 
также представлены как SgClassStmt. Но объявление: 
```cpp
A a; 
```
где A был объявлен как класс ранее, является [[SgVarDeclStmt]]. Как только класс определен, информация о его полях может быть обработана с помощью методов класса SgClassType. Если cls является указателем на SgClassStmt, то вы можете использовать 
```cpp
isSgClassType(cls->name()->type())
```
чтобы получить указатель на тип.
Примечание о том, как представлены суперклассы (также известные как базовые предложения в грамматике C++(_base-clauses_ in C++ grammar)). В определении:
```cpp
class A: public B, virtual private C {...};
```
список 
```cpp
public B, virtual private C
```
является базовым предложением.
До версии 1.9 Sage++ этот список хранился в виде EXPR_LIST, где каждое выражение представляло собой VAR_REF, переменной которого был символ имени класса. Спецификаторы public, virtual и т.д. были сохранены как тип T_DESCRIPT без базового класса; этот тип был присоединен к выражению VAR_REF.

Начиная с версии 1.9, представление базового предложения также представляет собой EXPR_LIST, содержащий выражения VAR_REF; однако теперь переменные являются "безымянными" символами (т.е. имена представляют собой пустые строки), а информация о классе и спецификаторах хранится в виде информации о типе (это аналогично представлению списка из безымянных аргументов в прототипе функции). Так, например,
```cpp
public B
```
представлен символом VAR_REF, у которого нет имени. Тип всего выражения и тип символа - T_DESCRIPT с заданным значением BIT_PUBLIC; базовый тип - T_DERIVED_TYPE, имя типа которого является символом для B.

Это представление ближе к семантике C++ и позволяет нам ссылаться на вложенные классы, как в
```cpp
class A: private Outer::Inner{};
```
Аналогично, для базовых классов шаблонов, как
```cpp
template<class T> class X:  public S<T> { 
	int j;
};
```
информация о
```cpp
public S<T>
```
хранится как информация о типе; в данном случае T_DESCRIPT, базовым классом которого является T_DERIVED_TEMPLATE, где имя шаблона является символом для S, а поле arguments содержит информацию о T. Раньше информация о T хранилась как о правильном дочернем элементе узла VAR_REF.

Кроме того, начиная с версии 1.9, анализатор не добавляет спецификатор public: автоматически. Например, до версии 1.9 
```cpp
class A: B{...}; 
```
преобразовался в 
```cpp
class A: public B{...}; 
```
Теперь он преобразуется в 
```cpp
class A: B{...}; 
```

Также обратите внимание, что старое поведение могло привести к ошибкам, поскольку базовый класс без явно указанного доступа - это не то же самое, что общедоступный доступ! Кроме того, в версиях 1.7 и более ранних была ошибка, из-за которой пустое определение класса, например, 
```cpp
class A{}; 
```
не соответствовало объявлению класса, 
```cpp
class A; 
```
Теперь оно не соответствует классу 
```cpp
A { public: };
```
Как вы можете видеть, размещение public: inside не идеально, но, похоже, это не смущает ни один из компиляторов C++. @sp 2 Добавлен новый метод, SgClassStmt::setSuperClass. Он принимает три аргумента: 
```cpp
void SgClassStmt::setSuperClass(int i, SgSymbol &type;_symb, int access) 
```
третий аргумент задает модификатор доступа; он должен быть одним из следующих: 
- BIT_PRIVATE, 
- BIT_PROTECTED, 
- BIT_PUBLIC, 
- BIT_PRIVATE, 
- BIT_VIRTUAL, 
- BIT_PROTECTED, 
- BIT_VIRTUAL, 
- BIT_PRIVATE 
- BIT_VIRTUAL.
#### Примеры
[[8 Expand Syntax - Init]]