Этот класс предоставляет доступ к локальным таблицам символов и типов, а также к определениям верхнего уровня в файле .dep, которому он соответствует.

```cpp
class  SgFile {

private:
    static std::map<std::string, std::pair<SgFile*, int> > files;

public:

    PTR_FILE filept;

    SgFile(char* file_name); // the file must exist.

    SgFile(int Language, const char* file_name); // for new empty file objects.

    ~SgFile();

    SgFile(SgFile &);

    inline int languageType();

    inline void saveDepFile(const char *dep_file);

    inline void unparse(FILE *filedisc);

    inline void unparsestdout();

    inline void unparseS(FILE *filedisc, int size);

    const char* filename();

  

    inline SgStatement *mainProgram();

    SgStatement *functions(int i);

    inline int numberOfFunctions();

    SgStatement *getStruct(int i);

    inline int numberOfStructs();

  

    inline SgStatement *firstStatement();

    inline SgSymbol *firstSymbol();

    inline SgType *firstType();

    inline SgExpression *firstExpression();

  

    inline SgExpression *SgExpressionWithId(int i);

    inline SgStatement *SgStatementWithId(int id);

    inline SgStatement *SgStatementAtLine(int lineno);

    inline SgSymbol *SgSymbolWithId(int id);

    inline SgType *SgTypeWithId(int id);

    // for attributes;

    void saveAttributes(char *file);

    void saveAttributes(char *file, void(*savefunction)(void *dat, FILE *f));

    void readAttributes(char *file);

    void readAttributes(char *file, void * (*readfunction)(FILE *f));

    int numberOfAttributes();

    SgAttribute *attribute(int i);

  

    /***** Kataev 15.07.2013 *****/

    int numberOfFileAttributes();

    int numberOfAttributes(int type); // of a specified type;

    void *attributeValue(int i);

    int  attributeType(int i);

    void *attributeValue(int i, int type); // only considering one type attribute

    void *deleteAttribute(int i);

    void addAttribute(int type, void *a, int size); // void * can be NULL;

    void addAttribute(int type); //void * is NULL;

    void addAttribute(void *a, int size); //no type specifed;

    void addAttribute(SgAttribute *att);

    SgAttribute *getAttribute(int i);

    SgAttribute *getAttribute(int i, int type);

    /*****************************/

  

    int expressionGarbageCollection(int deleteExpressionNode, int verbose);

    //int SgFile::expressionGarbageCollection(int deleteExpressionNode, int verbose);

  

    static int switchToFile(const std::string &name);

    static void addFile(const std::pair<SgFile*, int> &toAdd);    

};
```



####  Члены класса
Предоставляет доступ (открывает) к существующему файлу, обычно создаваемому синтаксическим анализатором.
Конструктор, получающий на вход указатель на начало строки с названием файла.
Открывает файл. Переключает процедуры на чтение указанного файла.
Добавляет файл в текущий проект, если проект существует. (Сайд эффект!)
Выдаёт номер файлу проекта и добавляет его в таблицу.
Для вызова этого конструктора предполагается, что файл должен существовать.
```cpp
SgFile::SgFile(char * dep_file_name) {
    filept = GetPointerOnFile(dep_file_name);
    SetCurrentFileTo(filept);
    SwitchToFile(GetFileNumWithPt(filept));

    if (!filept) {
        Message("File not found in SgFile; added", 0);
        if (CurrentProject)
            CurrentProject->addFile(dep_file_name);
    }

    SetMappingInTableForFile(filept, (void *)this);
#if __SPF
	addToCollection(__LINE__, __FILE__, this, 1);
#endif
}
```

Этот конструктор позволяет пользователю создать пустой файл .dep, чтобы позже вставлять в него инструкции. Подробное описание этого конструктора в разделе SgFileUsage (TODO) Использование SgFile.
```cpp
SgFile::SgFile(int Language, const char * dep_file_name) {

    if (new_empty_file(Language, dep_file_name) == 0) {
        Message("create failed", 0);
#ifdef __SPF
        char buf[512];
        sprintf(buf, "Internal error at line %d and file libSage++.cpp\n", __LINE__);
        addToGlobalBufferAndPrint(buf);
        throw -1;
#endif
    }

    filept = GetPointerOnFile(dep_file_name);
    SetCurrentFileTo(filept);
    SwitchToFile(GetFileNumWithPt(filept));
    if (!filept) {
        Message("File not found in SgFile; failed!", 0);
        
#ifdef __SPF  
        char buf[512];
        sprintf(buf, "Internal error at line %d and file libSage++.cpp\n", __LINE__);
        addToGlobalBufferAndPrint(buf);
        throw -1;
#endif

        return;
    }
    SetMappingInTableForFile(filept, (void *)this);
#if __SPF
    addToCollection(__LINE__, __FILE__, this, 1);
#endif

}
```

Возвращает `CSrc` (для C) или `ForSrc` (для Fortran).
```cpp
int languageType()
```

Сохраняет внутреннее представление файла как файл `.dep` с именем `dep_file`.
```cpp
void saveDepFile(char *dep_file)
```


Распаковывает внутреннее представление файла и сохраняет результат в файле с файловым дескриптором `filedisc`.
```cpp
void unparse(FILE *filedisc)
```


Выводит внутреннее представление файла в стандартный вывод.
```cpp
void unparsestdout()
```


Возвращает оператор в файле, в котором расположена основная программа, или `**NULL**`, если основная программа не находится в этом файле.
```cpp
SgStatement *mainProgram()
```


Возвращает i-ю функцию в файле.
```cpp
SgStatement *functions(int i)
```


Возвращает количество функций в файле.
```cpp
int numberOfFunctions()
```


Возвращает i-ю структуру (? или класс, или объединение?) в файле.
```cpp
SgStatement *getStruct(int i)
```


Возвращает количество структур в файле.
```cpp
int numberOfStructs()
```


Возвращает первый оператор в файле.
```cpp
SgStatement *firstStatement()
```


Возвращает первый символ в таблице символов файла.
```cpp
SgSymbol *firstSymbol()
```


Возвращает первый тип в таблице типов файла.
```cpp
SgType *firstType()
```


Возвращает первое выражение в файле.
```cpp
SgExpression *firstExpression()
```


Возвращает выражение в файле с идентификатором `i`.
```cpp
SgExpression *SgExpressionWithId(int i)
```


Возвращает оператор в файле с идентификатором `id`.
```cpp
SgStatement *SgStatementWithId( int id)
```


Возвращает оператор в строке `i` в файле.
```cpp
SgStatement *SgStatementAtLine(int lineno)
```


Возвращает символ в файле с идентификатором `id`.
```cpp
SgSymbol *SgSymbolWithId(int id)
```


Возвращает тип в файле с идентификатором `id`.
```cpp
SgType *SgTypeWithId( int id)
```


### Примеры
Обычно файл .dep создается синтаксическим анализатором, а программа Sage изменяет уже существующий файл .dep. Однако в некоторых ситуациях возникает необходимость в создании пустого файла .dep и последующем добавлении в него инструкций. В Sage++ версии 1.7 появился новый конструктор:
```cpp
     SgFile::SgFile(int Language, char * dep_file_name)
```
был добавлен. Его можно использовать для создания новых пустых файлов .dep. В приведенном ниже фрагменте кода показан пример использования:

```cpp
  SgProject project("x.proj");
  SgFile file(CSrc, "y.c");  // create a new file
  SgStatement *s = f->firstStatement();
  SgPointerType *p, *q;
  SgType *v;
  if(s == NULL) printf("no first statement\n");
  SgFuncHedrStmt *mane = new SgFuncHedrStmt("main");
  mane->AddArg("argc",*SgTypeInt());  // add int argc
  v = new SgPointerType(*SgTypeChar());
  q = new SgPointerType(*v);
  // note: new SgPointerType (*p) will not work,
  //  the reason is that the default copy constructor is called
  mane->AddArg("argv", *q); // char ** argv
  s->insertStmtAfter(*mane);
```
Обратите внимание, что "empty" файл, созданный конструктором SgFile, на самом деле не является полностью пустым: он содержит одну инструкцию (глобальный узел). Кроме того, чтобы приведенный выше пример работал, вам необходимо, чтобы файлы x.proj и x.dep находились в одном каталоге.

Обычно вы не создаете экземпляр SgFile самостоятельно. Скорее, вы создаете экземпляр проекта, а затем получаете доступ к файлам в проекте через элемент file() SgProject.

Существует два способа просмотра файла. Один из способов - получить доступ к каждой подпрограмме и функции с помощью методов numberOfFunctions() и functions(i). Например, чтобы вывести названия всех подпрограмм в проекте, вы можете попробовать:

```cpp
SgProject *project;
...
/* from Sage++ demo 'instrument', in function InitFunctionTable()) */

for (int i = 0; i < project->numberOfFiles(); i++) {
  SgFile *f;

  f = &(project->file(i));
    
  int num_routines;
    
  num_routines = f->numberOfFunctions();
  for (int j = 0; j < num_routines; j++){
      SgStatement *sub;
      SgSymbol *subsym;

      sub = f->functions(j);
      subsym = sub->symbol();

      printf("Function %d's name is %s\n", i*Files+j, subsym->identifier());
  }
}
```

Другой способ просмотреть файл - это получить к нему доступ в лексическом порядке, начиная с firstStatement(), как в:

```cpp
void traverseFile(SgFile *f) {
  SgStatement *s;

  for (s = f->firstStatement(); s; s = s->lexNext()) {
    /* Do something to the statement */
  }
  
}
```








Ссылки: [[SgStatement]], [[SgSymbol]], [[SgType]], [[SgExpression]], (SgAttribute).
