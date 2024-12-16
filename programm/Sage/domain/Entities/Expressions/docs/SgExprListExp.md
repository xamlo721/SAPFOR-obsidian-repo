Представляет списки выражений для всех языков.
```cpp
class **SgExprListExp**: public SgExpression {
        // variant == EXPR_LIST
public:
  inline SgExprListExp(PTR_LLND ll);
  inline SgExprListExp();
  inline SgExprListExp(SgExpression &ptr;);
  inline ~SgExprListExp();
  inline int length();
  inline SgExpression *elem(int i);
  inline SgExprListExp *next();
  inline SgExpression *value();
  inline void setValue(SgExpression &ptr;);      
  inline void append(SgExpression &arg;); //arg is a single element
                 // this is equiv. to (append this (list arg)) in Scheme
                 //use to add arg as the last element to the list
  void linkToEnd(SgExpression &arg;);  //arg should be a list
          // i.e.,  have type SgExprListExp
          //this works like append in Scheme
          //use to append arg as a list at the end of the given list
          //i.e, build a list consisting of the elements of the given
          //list followed by the elements of the arg list
          //if arg is not a list this produces a dotted pair
};
```

#### Члены класса

`**SgExprListExp**`**(PTR_LLND ll)**

document me

`**SgExprListExp**`**()**

document me

`**SgExprListExp**`**(SgExpression &ptr;)**

document me

`int **length**`**()**

document me

`SgExpression ***elem**`**(int i)**

document me

`SgExprListExp ***next**`**()**

document me

`SgExpression ***value**`**()**

document me

`void **setValue**`**(SgExpression &ptr;)**

document me

`void **append**`**(SgExpression &arg;)**

arg - это отдельный элемент. Это эквивалентно (добавить это (list arg)) в Scheme. Используйте этот метод, чтобы добавить arg в качестве последнего элемента в список.

`void **linkToEnd**`**(SgExpression &arg;)**

arg должен быть списком, то есть иметь тип SgExprListExp. Этот метод работает как append в Scheme. Используйте его, чтобы добавить arg в виде списка в конец данного списка, т.е. создать список, состоящий из элементов данного списка, за которыми следуют элементы списка arg. Если arg не является списком, это создает пунктирную пару.

#### Примеры
[[11 Instrument - VistaInstrument]]
[[21 Instrument - ListCollectionInvocations]]
[[25 Instrument - InsertCCallNode]]
[[26 Instrument - CTimingInstrumentSub]]
[[3 Expand Syntax - ExpandSyntax]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
