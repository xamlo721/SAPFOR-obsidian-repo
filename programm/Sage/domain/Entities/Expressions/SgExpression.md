SgExpression является базовым классом для всех остальных классов выражений. Каждое выражение может содержать до двух операндов (или subexpressions), левостороннее lhs() и правостороннее rhs(). Каждое выражение имеет тип type(), может содержать символ symbol() и уникальный идентификатор id().

```cpp
class  **SgExpression** {
public:
  PTR_LLND thellnd;
  // generic expression class.
  SgExpression(int variant, SgExpression &lhs;, SgExpression &rhs;,
               SgSymbol &s;, SgType &type;);

  SgExpression(int variant, SgExpression *lhs, SgExpression *rhs,
 	       SgSymbol *s, SgType *type);
  SgExpression(int variant, SgExpression *lhs, SgExpression *rhs,
 	       SgSymbol *s);
  // for some node in fortran
  SgExpression(int variant,char *str);

  SgExpression(int variant);
  SgExpression(PTR_LLND ll);
  inline SgExpression(SgExpression &);
  inline ~SgExpression();
  
  inline SgExpression *lhs();
  inline SgExpression *rhs();
  SgExpression *operand(int i);   //i=0,1
  inline int variant();      
  inline SgType *type(); 
  SgSymbol *symbol();
  inline int id();
  inline SgExpression *nextInExprTable();
  
  inline void setLhs(SgExpression &e;);
  inline void setLhs(SgExpression *e);
  inline void setRhs(SgExpression &e;);
  inline void setRhs(SgExpression *e);
  inline void setSymbol(SgSymbol &s;);
  inline void setSymbol(SgSymbol *s);
  inline void setType(SgType &t;);
  inline void setType(SgType *t);
  inline void setVariant(int v);
  
  inline SgExpression &copy();
  inline SgExpression *copyPtr();
  inline char *unparse(); 
  void sunparse(char *buffer);
  inline void unparsestdout();
  inline SgExpression *IsSymbolInExpression(SgSymbol &symbol;);
  inline void replaceSymbolByExpression(SgSymbol &symbol;, SgExpression &expr;);
  inline SgExpression *symbRefs();
  inline SgExpression *arrayRefs(); 
  int  linearRepresentation(int *coeff, SgSymbol **symb,int *cst, int size);
  SgExpression *normalForm(int n, SgSymbol *s);        
  SgExpression *coefficient(SgSymbol &s;); 
  int isInteger();
  int valueInteger();

friend SgExpression &operator; + ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; - ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; * ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; / ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; % ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; ^ ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; <<( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; >>( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; < ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; > ( SgExpression &lhs;, SgExpression &rhs;);
friend SgExpression &operator; <= ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; >= ( SgExpression &lhs;, SgExpression &rhs;);
friend SgExpression &operator; & ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; | ( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; &&( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; ||( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; +=( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; &=( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; *=( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; /=( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; %=( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; ^=( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; <<=( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &operator; >>=( SgExpression &lhs;, SgExpression &rhs;);
friend SgExpression &SgAssignOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgEqOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgNeqOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgExprListOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgRecRefOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgPointStOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgScopeOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgDDotOp;( SgExpression &lhs;, SgExpression &rhs;); 
friend SgExpression &SgBitNumbOp;( SgExpression &lhs;, SgExpression &rhs;); 

  /////////////// FOR ATTRIBUTES //////////////////////////

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

Обратите внимание, что SgExpression используется для представления основных двоичных операторов для C и Fortran, которые перечислены ниже вместе с их вариантами:

```cpp
+ ADD_OP
- SUBT_OP
* MULT_OP
/ DIV_OP
% MOD_OP

< LT_OP
> GT_OP
<= LE_OP
>= GE_OP

^ XOR_OP     bitwise exclusive-OR in C++, .XOR. in Fortran
& BITAND_OP
| BITOR_OP
&& AND_OP
|| OR_OP
<< LSHIFT_OP
>> RSHIFT_OP

= ASSGN_OP
+= PLUS_ASSGN_OP
&= AND_ASSGN_OP
*= MULT_ASSGN_OP
/= DIV_ASSGN_OP
%= MOD_ASSGN_OP
^= XOR_ASSGN_OP
<<= LSHIFT_ASSGN_OP
>>= RSHIFT_ASSGN_OP

== EQ_OP
!= NE_OP

-> POINTST_OP
:: SCOPE_OP
: BIT_NUMBER   in C++, for bit fields
```

#### Члены класса

`**SgExpression**`**(int variant, SgExpression &lhs;, SgExpression &rhs;, SgSymbol &s;, SgType &type;)**

document me

`**SgExpression**`**(int variant)**

document me

`**SgExpression**`**(PTR_LLND ll)**

document me

`SgExpression ***lhs**`**()**

document me

`SgExpression ***rhs**`**()**

document me

`SgExpression ***operand**`**(int i)**

Допустимо для i = 0, 1. В Sage++ версий 1.7 и более ранних i = 1, 2. Начиная с Sage++ версии 1.9 все аргументы, которые играют роль индексов, начинаются с нуля.

`int **variant**`**()**

document me

`SgType ***type**`**()**

document me

`SgSymbol ***symbol**`**()**

document me

`int **id**`**()**

document me

`SgExpression ***nextInExprTable**`**()**

document me

`void **setLhs**`**(SgExpression &e;)**

document me

`void **setRhs**`**(SgExpression &e;)**

document me

`void **setSymbol**`**(SgSymbol &s;)**

document me

`void **setType**`**(SgType &t;)**

document me

`void **setVariant**`**(int v)**

document me

`SgExpression &**copy**`**()**

Returns a deep copy.

`char ***unparse**`**()**

document me

`void **sunparse**`**(char *buffer)**

document me

`void **unparsestdout**`**()**

document me

`SgExpression ***IsSymbolInExpression**`**(SgSymbol &symbol;)**

Возвращает наиболее вложенное выражение, содержащее ссылку на символ.

`void **replaceSymbolByExpression**`**(SgSymbol &symbol;, SgExpression &expr;)**

document me

`SgExpression ***symbRefs**`**()**

document me

`SgExpression ***arrayRefs**`**()**

Возвращает список ссылок на массивы в выражении.

`int **linearRepresentation**`**(int *coeff, SgSymbol **symb,int *cst, int size)**

document me

`SgExpression ***normalForm**`**(int n, SgSymbol *s)**

Упрощается ли нормальная форма как линейная комбинация символов в s.

`SgExpression ***coefficient**`**(SgSymbol &s;)**

Находит мультипликативный коэффициент s в выражении.

`int **isInteger**`**()**

Истинно, если выражение может быть сведено к целочисленному значению.

`int **valueInteger**`**()**

Если isInteger() имеет значение true, возвращает целое значение, к которому может быть приведено выражение.

#### Использование

Стандартные бинарные операторы не имеют явных подклассов или конструкторов. Однако каждый из этих операторов был перегружен как \"friend\" класса SgExpression, поэтому построение выражений с помощью этих операторов является очень простой задачей. Например, для построения выражения вида
```cpp
     (X+3)*Y+6.4
```
программе нужны только два символа и два выражения значений:
```cpp
SgVariableSymb xsymb("X"), ysymb("Y");
SgVarRefExp x(xsymb), y(ysymb);
SgValueExp  three(3), fltvalue(6.4);
SgExpression &e; = (x + three)*y + fltvalue;
```
Переменные X и Y сначала создаются как символы, а затем выражения, которые являются ссылками на эти символы, создаются как объекты [[SgVarRefExp]]. Обратите внимание, что мы не указали типы для переменных X и Y, и объявления для X и Y еще не созданы.

В этом коде e теперь является ссылкой на корень (+) дерева синтаксического анализа для нужного выражения. Обратите внимание, что конструкторы для класса [[SgValueExp]] позволяют создавать литералы любого типа.
```cpp
SgExpression   SgAssignOp( SgExpression &lhs;, SgExpression &rhs;); 
SgExpression       SgEqOp( SgExpression &lhs;, SgExpression &rhs;); 
SgExpression      SgNeqOp( SgExpression &lhs;, SgExpression &rhs;); 
SgExpression  SgPointStOp( SgExpression &lhs;, SgExpression &rhs;); 
SgExpression    SgScopeOp( SgExpression &lhs;, SgExpression &rhs;);
```
Следовательно, для построения оператора присваивания на языке Си вида
```cpp
     X = (X+3)*Y+6.4
```
используя приведенные выше определения переменных X, Y, three и fltvalue, мы записываем
```cpp
     SgCExpStmt c_stmt(SgAssignOp(x.copy(), (x + three)*y + fltvalue));
```
В случае с Fortran обратите внимание, что присваивание является оператором, а не выражением. Чтобы создать тот же оператор в Fortran, мы пишем
```cpp
     SgAssignStmt fortran_stmt(x.copy(), (x + three)*y + fltvalue);
```
Все подклассы предназначены для предоставления удобных конструкторов, позволяющих легко создавать выражения и извлекать значения. Функция типа
```cpp
     SgSUBCLASS * isSgSUBCLASS( SgBASECLASS *)
```
он предусмотрен для каждого подкласса [[SgStatement]], SgExpression и [[SgType]]. Мы считаем, что этот механизм является эффективным способом использования строгой типизации в C++ для уменьшения количества ошибок.

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[11 Instrument - VistaInstrument]]
[[14 Instrument - isReferenceToMethodOfElement]]
[[15 Instrument - isReferenceToClassOfElement]]
[[21 Instrument - ListCollectionInvocations]]
[[26 Instrument - CTimingInstrumentSub]]
[[1 Expand Syntax - isReferenceToElementField]]
[[2 Expand Syntax - isArrayRefOfCollection]]
[[3 Expand Syntax - ExpandSyntax]]
[[4 Expand Syntax - SearchInExpForCollectionArrayRef]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[3 Dump Info - classifyStatements]]
[[6 Dump Info - doLoopStmts]]
[[13 Dump Info - classifyExpressions]]


