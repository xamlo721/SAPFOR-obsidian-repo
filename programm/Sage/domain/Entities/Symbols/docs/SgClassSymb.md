Представляет символы языка Си для обозначения класса, объединения, структуры и коллекции.
```cpp
class **SgClassSymb**: public SgSymbol {
  // the class, union, struct and collection type.
  // variant == CLASS_NAME, UNION_NAME, STRUCT_NAME or COLLECTION_NAME
public:
  inline SgClassSymb(int variant, char *name, SgStatement &scope;);
  inline ~SgClassSymb();
  inline int numberOfFields();
  inline SgSymbol *field(int i); //i=0,1,...
};
```

#### Члены класса
`**SgClassSymb**`**(int variant, char *name, SgStatement &scope;)**

document me


`int **numberOfFields**`**()**
Возвращает количество участников. Полезную информацию смотрите в описании метода SgSymbol \* field(int i).


`SgSymbol ***field**`**(int i)**

Возвращает i-й элемент. Начиная с версии 1.9, параметр i начинается с нуля (в версиях 1.7 и более ранних он начинался с единицы). Определение того, что представляет собой поле для целей методов numberOfFields и field, несколько необычно. Рассмотрим следующий пример:
```cpp
class foo;
class X{ public: void xmember();};

class test{
  public:
    int i, j, k; // data members
    static istat;
    friend test operator+(const test&, const test&);
    friend class foo;
    friend class foo;
    friend void X::xmember();
    class I1;   //forward decl. of nested class
    int fint(int);  //member function
    typedef int Myint;  //nested type
    class inner{}; //nested type
    enum dir{left='l',right='r'};  //left and right are member constants
  };

```

В этом случае Sage++ отображает следующие поля:
```cpp
number of fields  11
field no. 0 symbol  i
field no. 1 symbol  j
field no. 2 symbol  k
field no. 3 symbol  istat
field no. 4 symbol  +
field no. 5 symbol  fint
field no. 6 symbol  Myint
field no. 7 symbol  inner
field no. 8 symbol  dir
field no. 9 symbol  left
field no. 10 symbol  right
```



Для SgClassSymb, представляющего класс, который уже был определен, функция type() возвращает указатель на SgClassType (т.е. isSgClassType(symb->type()) должен возвращать ненулевой указатель на SGCLASSSTYPE). Класс SgClassType содержит метод SgStatement \*structureDecl(), который можно использовать для доступа к инструкции, содержащей определение класса.