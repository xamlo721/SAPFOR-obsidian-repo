Представляет основной класс для всех операторов.

```cpp
// Discuss about control parent, BIF structure etc
class  SgStatement 
{
private:
    int fileID;
    SgProject *project;
    bool unparseIgnore;

    static bool sapfor_regime;
    static std::string currProcessFile;
    static int currProcessLine;
    static bool deprecatedCheck;
    static bool consistentCheckIsActivated;
    // fileID -> [ map<FileName, line>, SgSt*]
    static std::map<int, std::map<std::pair<std::string, int>, SgStatement*> > statsByLine;
    static void updateStatsByLine(std::map<std::pair<std::string, int>, SgStatement*> &toUpdate);
    static std::map<SgExpression*, SgStatement*> parentStatsForExpression;
    static void updateStatsByExpression();
    static void updateStatsByExpression(SgStatement *where, SgExpression *what);

    void checkConsistence();
    void checkDepracated();
    void checkCommentPosition(const char* com);

public:
    PTR_BFND thebif;
    SgStatement(int variant);
    SgStatement(PTR_BFND bif);
    SgStatement(int code, SgLabel *lab, SgSymbol *symb, SgExpression *e1 = NULL, SgExpression *e2 = NULL, SgExpression *e3 = NULL);
    SgStatement(SgStatement &);
    // info about statement
    inline int lineNumber();          // source text line number
    inline int localLineNumber();
    inline int id();                  // unique id;
    inline int variant();             // the type of the statement
    SgExpression *expr(int i); // i = 0,1,2 returns the i-th expression.

    inline int hasSymbol();  // returns TRUE if tmt has symbol, FALSE otherwise
    // returns the symbol field. Used by loop headers to point to the
    // loop variable symbol; Used by function and subroutine headers to
    // point to the function or subroutine name.
    SgSymbol *symbol();        // returns the symbol field.
    inline char *fileName();
    inline void setFileName(char *newFile);

    inline int hasLabel();     // returns 1 if there is a label on the stmt.
    SgLabel *label();          // the label

    // modifying the info.
    inline void setlineNumber(const int n); // change the line number info
    inline void setLocalLineNumber(const int n);
    inline void setId(int n);         // cannot change the id info
    inline void setVariant(int n);    // change the type of the statement
    void setExpression(int i, SgExpression &e); // change the i-th expression
    void setExpression(int i, SgExpression *e); // change the i-th expression
    inline void setLabel(SgLabel &l); // change the label
    inline void deleteLabel(bool saveLabel = false); // delete label
    inline void setSymbol(SgSymbol &s); // change the symbol

    // Control structure
    inline SgStatement *lexNext();   // the next statement in lexical order.
    inline SgStatement *lexPrev();   // the previous stmt in lexical order.
    inline SgStatement *controlParent(); // the enclosing control statement

    inline void setLexNext(SgStatement &s); // change the lexical ordering
    inline void setLexNext(SgStatement* s);

    // change the control parent.
    inline void setControlParent(SgStatement& s) // DEPRECATED IN SAPFOR!! 
    {
        checkDepracated();
        BIF_CP(thebif) = s.thebif; 
    }

    inline void setControlParent(SgStatement* s) // DEPRECATED IN SAPFOR!!
    {
        checkDepracated();
        if (s != 0)
            BIF_CP(thebif) = s->thebif;
        else
            BIF_CP(thebif) = 0;
    }

  // Access statement using the tree structure
  // Describe BLOB lists here?

    inline int numberOfChildrenList1();
    inline int numberOfChildrenList2();
    inline SgStatement *childList1(int i);
    inline SgStatement *childList2(int i);
    SgStatement *nextInChildList();

    inline SgStatement *lastDeclaration();
    inline SgStatement *lastExecutable();
    inline SgStatement *lastNodeOfStmt();
    inline SgStatement *nodeBefore();
    inline void insertStmtBefore(SgStatement &s, SgStatement &cp);
    void insertStmtAfter(SgStatement &s, SgStatement &cp);

    inline void insertStmtBefore(SgStatement& s)  // DEPRECATED IN SAPFOR!!
    {
        checkDepracated();
        insertBfndBeforeIn(s.thebif, thebif, NULL); 
    }
    inline void insertStmtAfter(SgStatement& s) // DEPRECATED IN SAPFOR!!
    {
        checkDepracated();
        insertBfndListIn(s.thebif, thebif, NULL); 
    }

    inline SgStatement *extractStmt();
    inline SgStatement *extractStmtBody();
    inline void replaceWithStmt(SgStatement &s);
    inline void deleteStmt();
    inline SgStatement  &copy(void);
    inline SgStatement  *copyPtr(void);
    inline SgStatement  &copyOne(void);
    inline SgStatement  *copyOnePtr(void);
    inline SgStatement  &copyBlock(void);
    inline SgStatement  *copyBlockPtr(void);
    inline SgStatement  *copyBlockPtr(int saveLabelId);
    inline int isIncludedInStmt(SgStatement &s);
    inline void replaceSymbByExp(SgSymbol &symb, SgExpression &exp);
    inline void replaceSymbBySymb(SgSymbol &symb, SgSymbol &newsymb);
    inline void replaceSymbBySymbSameName(SgSymbol &symb, SgSymbol &newsymb);
    inline void replaceTypeInStmt(SgType &old, SgType &newtype);
    char* unparse(int lang = 0); // FORTRAN_LANG
    inline void unparsestdout();
    std::string sunparse(int lang = 0); // FORTRAN_LANG
    inline char *comments();      //preceding comment lines.
    void addComment(const char *com);
    void addComment(char *com);
    /* ajm: setComments: set ALL of the node's comments */
    inline void setComments(char *comments);
    inline void setComments(const char *comments);
    inline void delComments();
    int numberOfComments(); //number of preceeding comments. CAREFUL! 

    int hasAnnotations();   //1 if there are annotations; 0 otherwise
    ~SgStatement();
    // These function must be removed. Doesn't make sense here.
    int IsSymbolInScope(SgSymbol &symb); // TRUE if symbol is in scope
    int IsSymbolReferenced(SgSymbol &symb);
    inline SgStatement *getScopeForDeclare(); // return where a variable can be declared;

    /////////////// FOR ATTRIBUTES //////////////////////////

    int numberOfAttributes();
    int numberOfAttributes(int type); // of a specified type;
    void *attributeValue(int i);
    int  attributeType(int i);
    void *attributeValue(int i, int type); // only considering one type attribute
    void *deleteAttribute(int i);
    void addAttribute(int type, void *a, int size); // void * can be NULL;
    void addAttribute(int type); //void * is NULL;
    void addAttribute(void *a, int size); //no type specifed;
    void addAttribute(SgAttribute *att);
    void addAttributeTree(SgAttribute *firstAtt);
    SgAttribute *getAttribute(int i);
    SgAttribute *getAttribute(int i, int type);

    //////////// FOR DECL_SPECS (friend, inline, extern, static) ////////////

    inline void addDeclSpec(int type);   //type should be one of BIT_EXTERN,
                                  //BIT_INLINE, BIT_FRIEND, BIT_STATIC
    inline void clearDeclSpec();        //resets the decl_specs field to zero
    inline int isFriend();               //returns non-zero if friend modifier set
                                  //returns zero otherwise
    inline int isInline();
    inline int isExtern();
    inline int isStatic();

    // new opportunities were added by Kolganov A.S. 16.04.2018
    inline int getFileId() const { return fileID; }
    inline void setFileId(const int newFileId) { fileID = newFileId; }

    inline SgProject* getProject() const { return project; }
    inline void setProject(SgProject *newProj) { project = newProj; }

    inline bool switchToFile()
    {
        if (fileID == -1 || project == NULL)
            return false;

        if (current_file_id != fileID)
        {
            SgFile* file = &(project->file(fileID));
            currProcessFile = file->filename();
            currProcessLine = 0;
        }
        return true;
    }

    inline SgFile* getFile() const 
    { 
        if (fileID == -1 || project == NULL)
            return NULL;
        else
            return &(project->file(fileID)); 
    }

    inline void setUnparseIgnore(bool flag) { unparseIgnore = flag; }
    inline bool getUnparseIgnore() const { return unparseIgnore; }

    static SgStatement* getStatementByFileAndLine(const std::string &fName, const int lineNum);
    static void cleanStatsByLine() { statsByLine.clear(); }

    static SgStatement* getStatmentByExpression(SgExpression*);
    static void cleanParentStatsForExprs() { parentStatsForExpression.clear(); }
    static void activeConsistentchecker() { consistentCheckIsActivated = true; }
    static void deactiveConsistentchecker() { consistentCheckIsActivated = false; }
    static void activeDeprecatedchecker() { deprecatedCheck = true; }
    static void deactiveDeprecatedchecker() { deprecatedCheck = false; }

    static void setCurrProcessFile(const std::string& name) { currProcessFile = name; }
    static void setCurrProcessLine(const int line) { currProcessLine = line; }
    static std::string getCurrProcessFile() { return currProcessFile; }
    static int getCurrProcessLine() { return currProcessLine; }

    static void setSapforRegime() { sapfor_regime = true; }
    static bool isSapforRegime() { return sapfor_regime; }
};
```

####  Члены класса
Создает SgStatement с вариантом `variant`.
`**SgStatement**`**(int variant)**


Возвращает SgStatement, соответствующий узлу bif `bif`.
`**SgStatement**`**(PTR_BFND bif)**


Возвращает номер строки оператора в исходном файле.
`int **lineNumber**`**()**


Возвращает **_id_** выражения.
`int **id**`**()**


Возвращает **_variant_** оператора, который можно использовать для определения того, какой тип оператора на самом деле.
`int **variant**`**()**


Возвращает выражение `i` оператора. (Обратите внимание, что `i = 0, 1, 2`). С оператором может быть связано до трех выражений. Например, цикл C for имеет форму `for(expr_1; expr_2; expr_3)`.
`SgExpression ***expr**`**(int i)**


Возвращает ненулевое значение, если с оператором связан символ.
`int **hasSymbol**`**()**


Если с оператором связан символ, эта функция возвращает его. Этот символ используется для имени подпрограммы в операторе заголовка подпрограммы и, только в Fortran, для переменной индукции цикла DO.
`SgSymbol ***symbol**`**()**


Возвращает имя вложенного файла.
`char ***fileName**`**()**


Возвращает ненулевое значение, если с оператором связана метка.
`int **hasLabel**`**()**


Если у оператора есть метка, эта функция возвращает ее.
`SgLabel ***label**`**()**


Устанавливает номер строки оператора.
`void **setlineNumber**`**(int n)**


Устанавливает **_id_** выражения.
`void **setId**`**(int n)**


Устанавливает **_вариант_** оператора.
`void **setVariant**`**(int n)**


Устанавливает `i`-е выражение оператора в `e` (см. обсуждение выражений, связанных с оператором, в разделе `expr()` выше).
`void **setExpression**`**(int i, SgExpression &e;)**


Устанавливает метку оператора.
`void **setLabel**`**(SgLabel &l;)**


Устанавливает символ оператора.
`void **setSymbol**`**(SgSymbol &s;)**


Возвращает лексический последующий оператор оператора.
`SgStatement ***lexNext**`**()**


Возвращает лексический предшествующий оператор оператора.
`SgStatement ***lexPrev**`**()**


Возвращает оператор родительского элемента управления данного оператора.
`SgStatement ***controlParent**`**()**


Устанавливает лексический оператор-последователь данного оператора.
`void **setLexNext**`**(SgStatement &s;)**


Устанавливает родительский оператор управления этого оператора.
`void **setControlParent**`**(SgStatement &s;)**


Возвращает количество дочерних элементов в первом списке дочерних элементов этого оператора.
`int **numberOfChildrenList1**`**()**


Возвращает количество дочерних элементов во втором списке дочерних элементов этого оператора.
`int **numberOfChildrenList2**`**()**


Возвращает i-й оператор в первом списке дочерних операторов данного оператора.
`SgStatement ***childList1**`**(int i)**


Возвращает i-й оператор во втором списке дочерних операторов этого оператора.
`SgStatement ***childList2**`**(int i)**


Возвращает следующий оператор в списке дочерних операторов этого оператора. (? следующий после чего?)
`SgStatement ***nextInChildList**`**()**


Если оператор не является листом дерева разбора, эта функция возвращает последнее объявление в поддереве, которое определяет оператор. Этот метод бесполезен в C++.
`SgStatement ***lastDeclaration**`**()**


Если оператор не является листом дерева разбора, эта функция возвращает последний исполняемый оператор в поддереве, которое определяет оператор. Этот метод бесполезен в C++.
`SgStatement ***lastExecutable**`**()**


Если оператор не является листом дерева синтаксического анализа, эта функция возвращает указатель на последний оператор в определяемом им поддереве.
`SgStatement ***lastNodeOfStmt**`**()**


(? в чем разница между этим и lexPrev?)
`SgStatement ***nodeBefore**`**()**


Вставляет оператор `s` перед данным.
`void **insertStmtBefore**`**(SgStatement &s;)**


Вставляет оператор `s` перед этим. Устанавливает родительский элемент управления `s` в `cp`. (? это правильно?)
`void **insertStmtBefore**`**(SgStatement &s;, SgStatement &cp;)**


Вставляет оператор `s` после этого.
`void **insertStmtAfter**`**(SgStatement &s;)**


Вставляет оператор `s` после этого. Устанавливает родительский элемент управления `s` в `cp`. (? это правильно?)
`void **insertStmtAfter**`**(SgStatement &s;, SgStatement &cp;)**


Удаляет этот оператор из дерева синтаксического анализа и возвращает указатель на удаленный оператор.
`SgStatement ***extractStmt**`**()**


Если оператор не является листом дерева синтаксического анализа, эта функция извлекает определяемое ею поддерево из дерева синтаксического анализа и возвращает указатель на первый оператор в дереве. (? это правильно?)
`SgStatement ***extractStmtBody**`**()**


Заменяет это утверждение утверждением `s`.
`void **replaceWithStmt**`**(SgStatement &s;)**


Удаляет этот оператор из дерева синтаксического анализа и освобождает связанную с ним память.
`void **deleteStmt**`**()**


document me
`SgStatement &**copy**`**()**


document me
`SgStatement ***copyPtr**`**()**


document me
`SgStatement &**copyOne**`**()**


document me
`SgStatement ***copyOnePtr**`**()**


document me
`SgStatement &**copyBlock**`**()**


document me
`SgStatement ***copyBlockPtr**`**()**


document me
`int **isIncludedInStmt**`**(SgStatement &s;)**


document me
`void **replaceSymbByExp**`**(SgSymbol &symb;, SgExpression &exp;)**


document me
`void **replaceSymbBySymb**`**(SgSymbol &symb;, SgSymbol &newsymb;)**


document me
`void **replaceSymbBySymbSameName**`**(SgSymbol &symb;, SgSymbol &newsymb;)**


document me
`void **replaceTypeInStmt**`**(SgType &old;, SgType &newtype;)**


document me
`char* **unparse**`**()**


document me
`void **unparsestdout**`**()**


document me
`void **sunparse**`**(char *buffer)**


Предыдущие комментарии прилагаются справа от заявления.
`char ***comments**`**()**


document me
`void **addComment**`**(char *com)**


document me
`void **setComment**`**(char *commments)**


document me
`int **numberOfComments**`**()**


document me
`int **hasAnnotations**`**()**


document me
`int **IsSymbolInScope**`**(SgSymbol &symb;)**


document me
`int **IsSymbolReferenced**`**(SgSymbol &symb;)**


document me
`SgStatement ***getScopeForDeclare**`**()**


document me
`void **addDeclSpec**`**(int type)**


document me
`void **clearDeclSpec**`**()**


document me
`int **isFriend**`**()**


document me
`int **isInline**`**()**


document me
`int **isExtern**`**()**


document me
`int **isStatic**`**()**


### Примеры
Оператор может содержать до двух списков дочерних операторов. Например, для оператора if все операторы в ветви "true" принадлежат childList1, а все операторы в ветви "false" принадлежат childList2. Что касается определений функций, то все операторы в теле функции принадлежат childList1.

После извлечения инструкции из дерева синтаксического анализа можно создать ее копию с помощью функции copy() и вставить копию или оригинал в другую позицию. Например, S1.insertStmtAfter(S2) вставит S2 в лексическую позицию, следующую за S1.

Можно также выполнить поиск символа в выражении и его подвыражениях и заменить все вхождения другим символом или выражением. Аналогично, можно заменить любую ссылку на данный тип другим типом.

Чтобы проиллюстрировать использование классов операторов, рассмотрим следующий простой пример. Предположим, мы хотим просмотреть файл и применить разворачивающее преобразование ко всем внутренним циклам most, тело которых состоит только из операторов присваивания. Функция, которая выполняет это, показана ниже

```cpp
void UnrollLoops(SgFile *file, int unroll_factor){
   SgStatement *s = file->firstStatement();
   SgForStmt *loop;
   while(s){
      if(loop = isSgForStmt(s)){
          if(loop->isAssignLoop()) loop->unrollLoop(unroll_factor);
          }
      s = s->lexNext();
   }
}
```
Эта функция иллюстрирует важный аспект стиля программирования, используемого в Sage++. Основная часть функции представляет собой цикл, который просматривает инструкции в файле в лексическом порядке. Переменная s является указателем на общий объект statement. Есть два способа определить, является ли оператор циклом. Один из них - проверить, является ли параметр FOR_NODE. Другой способ - использовать специальную функцию приведения, в данном случае isSgForStmt(), которая проверит вариант и вернет указатель, приведенный к правильному подклассу, или NULL, если он не соответствует. Поскольку C++ является строго типизированным языком, если мы хотим применить методы подкласса, такое приведение необходимо. Функция типа
```cpp
     SgSUBCLASS * isSgSUBCLASS( SgBASECLASS *)
```
он предусмотрен для каждого подкласса SgStatement, [[SgExpression]] и [[SgType]]. Мы считаем, что этот механизм является эффективным способом использования строгой типизации в C++ для уменьшения количества ошибок.

Методы copyBlock() и \*copyBlockPtr() копируют все остальные операторы в текущем блоке (т.е. с тем же родительским элементом управления, что и у данного оператора), включая данный оператор. Все дочерние операторы также копируются. Предупреждение: такие вещи, как блочное копирование инструкции, которая сама по себе является блочной копией чего-то другого, не будут работать, поскольку инструкция, возвращаемая функцией copyBlock(), не имеет родительского элемента управления.

Методы addDeclSpec(тип int), clearDeclSpec(), isFriend(), isInline(), isExtern() и isStatic() используются для обработки спецификаторов friend, extern, static и inline. В более старых версиях Sage++ это были модификаторы узлов типа. Начиная с июля 1994 года, они являются модификаторами узлов инструкции (bif). Чтобы задать определенный модификатор, используйте один из BIT_EXTERN, BIT_INLINE, BIT_FRIEND или BIT_STATIC.

Вот пример, иллюстрирующий использование этих методов:

```cpp
#include <sage++user.h> 

 main() {
 
 	SgProject project("demo.proj");

 	for (int i = 0; i < project.numberOfFiles(); i++){
 	    printf (" current file is %s\n", project.fileName(i));
 	    SgFile *f;
 	    f = &(project.file(i));
 	    SgStatement *s; 

 	    for ( s = f->firstStatement(); s; s = s->lexNext()){
                if(s->isFriend())
                     printf("friend found in stmt with id %i-B\n",s->id());
                if(s->isInline()) 
                     printf("inline found in stmt with id %i-B\n",s->id());
                if(s->isStatic()) 
                     printf("static found in stmt with id %i-B\n",s->id());
                if(s->isExtern()) 
                     printf("extern found in stmt with id %i-B\n",s->id());
   		      s->clearDeclSpec();
 	    }
         f->unparsestdout();
     }
 }
```

Примеры использования:
[[2 Restructure - addStuffToProgram]]
[[3 Instrument - InitFunctionTable]]
[[4 Instrument - InsertFCallNode]]
[[5 Instrument - FixLoops]]
[[6 Instrument - FInstrumentSub]]
[[8 Instrument - FInstrument]]
[[10 Instrument - UnparseSub]]
[[11 Instrument - VistaInstrument]]
[[12 Instrument - FAnalyze]]
[[16 Instrument - inMethodOfTheElement]]
[[17 Instrument - whichFunctionAmI]]
[[18 Instrument - isReferenceToCollection]]
[[19 Instrument - ListCollections]]
[[20 Instrument - ListCollectionInstances]]
[[21 Instrument - ListCollectionInvocations]]
[[25 Instrument - InsertCCallNode]]
[[26 Instrument - CTimingInstrumentSub]]
[[4 Expand Syntax - SearchInExpForCollectionArrayRef]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[8 Expand Syntax - Init]]
[[3 Dump Info - classifyStatements]]
[[4 Dump Info - doRoutineHeader]]
[[5 Dump Info - doIfStmts]]
[[6 Dump Info - doLoopStmts]]
[[7 Dump Info - doIOStmts]]
[[8 Dump Info - doGoToStmt]]
[[9 Dump Info - doVarDecl]]

