SgSymbol является базовым классом для классов, представляющих символы. Как и в случае с другими классами, существует функция variant(), которая идентифицирует подкласс, и целочисленный идентификатор id(), уникальный для каждого символа. Символы в каждом файле упорядочены в виде списка, доступ к которому можно получить из объекта file как SgFile::firstSymbol(), а следующий за текущим символ находится с помощью next(). Каждый символ имеет идентификатор символьной строки(), тип(), который подробно описан ниже, и оператор scope(), который является оператором, в котором объявляется область действия. Область действия является родительским элементом управления для оператора declaration.

Кроме того, существуют функции, которые можно использовать для создания копии символа. Существует три формы копии. Базовая копия создает простую копию записи в таблице символов. Копия первого уровня также генерирует информацию о новом типе. Копия второго уровня также копирует текст декларации.

```cpp
class **SgSymbol** {
public:
  // basic class contains
  PTR_SYMB thesymb;
  SgSymbol(int variant, char *identifier, SgType &t;, SgStatement &scope;);
  SgSymbol(int variant, char *identifier, SgType *t, SgStatement *scope);
  SgSymbol(int variant, char *identifier,  SgStatement &scope;);
  SgSymbol(int variant, char *identifier,  SgStatement *scope);
  SgSymbol(int variant, char *identifier,   SgType *type, SgStatement *scope, 
           SgSymbol *structsymb, SgSymbol *nextfield );

  SgSymbol(int variant, char *name);
  SgSymbol(int variant);
  SgSymbol(PTR_SYMB symb);
  inline SgSymbol(SgSymbol &);
  ~SgSymbol();
  inline int variant();  
  inline int id();             // unique identifier
  inline char *identifier();   // the text name for the symbol.
  inline SgType *type();       // the type of the symbol
  inline void setType(SgType &t;);       // the type of the symbol
  inline void setType(SgType *t);       // the type of the symbol
  inline SgStatement *scope(); // the SgControlStatement where defined.
  inline SgSymbol *next();     // next symbol reference.
  SgStatement *declaredInStmt();  // the declaration statement
  inline SgSymbol &copy();
  inline SgSymbol &copyLevel1(); // copy also parameters
  inline SgSymbol &copyLevel2(); // copy parameters, body also
  inline SgSymbol &copyAcrossFiles(SgStatement &where;); // special copy to
                                                    // move things from a file.
  int attributes();    // the Fortran 90 attributes
  void setAttribute(int attribute);
  void removeAttribute(int attribute);
  void declareTheSymbol(SgStatement &st;);
  inline void declareTheSymbolWithParamList
                          (SgStatement &st;, SgExpression &parlist;);
  SgExpression *makeDeclExpr();
  inline SgExpression *makeDeclExprWithParamList
                          (SgExpression &parlist;);
  SgVarDeclStmt *makeVarDeclStmt();
  SgVarDeclStmt *makeVarDeclStmtWithParamList
                          (SgExpression &parlist;);
 
  SgStatement *body(); // the body of the symbol if has one (like, function 
                       // call, class,...)

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
}
```


#### Члены класса

`**SgSymbol**`**(int variant, char *identifier, SgType &t;, SgStatement &scope;)**

document me

`**SgSymbol**`**(int variant, char *identifier, SgStatement &scope;)**

document me

`**SgSymbol**`**(int variant, char *name)**

document me

`**SgSymbol**`**(int variant)**

document me

`**SgSymbol**`**(PTR_SYMB symb)**

document me

`int **variant**`**()**

document me

`int **id(**`**)**

document me

`char ***identifier**`**()**

document me

`SgType ***type**`**()**

document me

`void **setType**`**(SgType &t;)**

document me

`SgStatement ***scope**`**()**

document me

`SgSymbol ***next**`**()**

document me

`SgStatement ***declaredInStmt**`**()**

Предполагается, что этот метод возвращает указатель на инструкцию, в которой был объявлен данный символ. Однако в своей текущей реализации метод работает очень медленно (при каждом вызове выполняется линейный поиск по списку инструкций) и ненадежно. Часто бывает лучше написать дополнительные инструкции pass through и прикрепить информацию об инструкциях declaration к SgSymbols, используя SgAttribute, чтобы в дальнейшем эту информацию можно было просто искать, а не пересчитывать каждый раз, когда это необходимо.

`SgSymbol &**copy**`**()**

document me

`SgSymbol &**copyLevel1**`**()**

document me

`SgSymbol &**copyLevel2**`**()**

document me

`int **attributes**`**()**

document me

`void **setAttribute**`**(int attribute)**

document me

`void **removeAttribute**`**(int attribute)**

document me

`void **declareTheSymbol**`**(SgStatement &st;)**

Этот метод создает инструкцию объявления для данного символа и вставляет ее в верхнюю часть области, заданной st. Пожалуйста, смотрите раздел SgMakeDeclExp и связанные с ним методы для получения дополнительной информации об этом методе и других методах создания объявлений.

`void **declareTheSymbolWithParamList**`**(SgStatement &st;)**

Аналогично функции declareTheSymbol(), но принимает второй аргумент, который является списком параметров (для прототипов функций).

`SgExpression ***makeDeclExpr**`**()**

Создает выражение объявления и возвращает его.

`SgExpression ***makeDeclExprWithParamList**`**(SgExpression &parlist;)**

Аналогично makeDeclExpr(), но принимает второй аргумент, который является списком параметров (для прототипов функций).

`SgVarDeclStmt ***makeVarDeclStmt**`**()**

Создает оператор declaration и возвращает его (без вставки в файл)

`SgVarDeclStmt ***makeVarDeclStmtWithParamList**`**(SgExpression &parlist;)**

Аналогично makeVarDeclStmt(), но принимает второй аргумент, который является списком параметров (для прототипов функций).

`SgStatement ***body**`**()**

Если символ ссылается на функцию, структуру, подпрограмму или класс, то возвращается указатель на объект SgStatement, который является объявлением символа.


#### Использование

В качестве примера того, как просмотреть таблицу символов, рассмотрим задачу поиска записи в таблице символов для данной функции-члена в данном классе. Существует несколько способов сделать это. Схема, показанная ниже, позволяет выполнить поиск класса в таблице по имени. Затем он выполняет поиск функции-члена в списке полей и возвращает указатель на объект symbol, если он найден.

```cpp
SgSymbol *memberFunction(char *className, char *functionName){
  SgSymbol *s, *fld;
  SgClassSymb *cl;
  SgMemberFuncSymb *f;
  int i;

  for (s=file.firstSymbol(); s ; s = s->next())
    if (!strcmp(s->identifier(), className))
       break;

  if (s == NULL) 
     return NULL;

  if (cl = isSgClassSymb(s)){
    i = 1;
    while(fld = cl->field(i++)){
      if ((f = isSgMemberFuncSymb(fld)) &&
          !strcmp(f->identifier(), functionName)) 
         return f;
    }
  }
  return NULL;
}
```
В качестве другого примера рассмотрим задачу создания временных переменных, которые соответствуют типу и начальным параметрам конструктора данной переменной symbol. Более конкретно, рассмотрим объявления
```cpp
int *x[100], y[34];
myClass object(parm1, parm2);
```
Каждый из этих операторов относится к классу [[SgVarDeclStmt]], который имеет тип и список выражений. В первом случае список выражений содержит два элемента (называемых значениями в [[SgExprListExp]]): x\[100\], y\[34\], а во втором объявлении содержится один объект item(parm1, parm2). Следующая функция создает новый временный символ с именем \_Ti, где i - целочисленный счетчик, и задает запись в таблице символов, находит объявление символа и создает идентичное объявление для временного символа.
```cpp
char name_counter = '0';
SgSymbol * DeclareTemporaryLike(SgSymbol * x){
   SgStatement  *old_decl_stmt;
   SgSymbol *tmp;
   SgVarDeclStmt *decl_stmt;
   SgExpression *exp;
   char *name;
   SgExprListExp *elist;

   // now find the declaration statement for x and get
   // the correct initializing expression.
   old_decl_stmt = x.declaredInStmt()
      // get the expression list of variables delcared
   exp = old_decl_stmt->expr(0);

   // look for the reference to our symbol x.
   while(elist = isSgExprListExp(exp)){
	if((elist->value())->isSymbolInExpression(*x) 
            break;
        exp = elist->next();
	}    
   if(exp == NULL) return NULL;

   // now create a new expression list and 
   // and a new declaration statement
   elist = new SgExprListExp(*(exp->copy());
   decl_stmt = new SgVarDeclStmt(*elist,old_decl_stmt->type());

   // create a new variable of the same class
   // generate the name as "_Ti" where i is counter.
   name = new char(10);
   sprintf(name, "_T%c", name_counter++);
   tmp = new SgVariableSymb(name, (x->type())->copy(), *scope);

   // replace x with the new variable and insert
   // the new decl statement after the old one.
   decl_stmt->replaceSymbBySymb(*x, *tmp);
   old_decl_stmt->insertStmtAfter(*decl_stmt);
   return tmp;
}
```

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[1 Instrument - Fortran Program Transformations]]
[[3 Instrument - InitFunctionTable]]
[[4 Instrument - InsertFCallNode]]
[[14 Instrument - isReferenceToMethodOfElement]]
[[15 Instrument - isReferenceToClassOfElement]]
[[18 Instrument - isReferenceToCollection]]
[[21 Instrument - ListCollectionInvocations]]
[[25 Instrument - InsertCCallNode]]
[[26 Instrument - CTimingInstrumentSub]]
[[1 Expand Syntax - isReferenceToElementField]]
[[4 Expand Syntax - SearchInExpForCollectionArrayRef]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[8 Expand Syntax - Init]]
[[3 Dump Info - classifyStatements]]
[[4 Dump Info - doRoutineHeader]]
[[10 Dump Info - doSymb]]
[[11 Dump Info - doSymbAttribs]]
[[14 Dump Info - classifySymbols]]

