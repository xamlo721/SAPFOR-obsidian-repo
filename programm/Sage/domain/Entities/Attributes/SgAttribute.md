Представляет базовый класс атрибутов.
```cpp
class SgAttribute{
 private:
  // the attribute data;
  int type; // a label;
  void *data;  // the data;
  int dataSize; // the size of the data in bytes to allow data to be copied;
  SgAttribute *next; // to the next attribute of a statements (do that way 
                     // or not??);
  // link to sage node, allow to go from an attribute to sage stuffs;
  typenode typeNode;   // indicates if SgStatement, SgExpression, ... 
                       // ptToSage is pointed to;
  void *ptToSage; // pointer to SgStatement, SgExpression, ... ;
  int fileNumber; // the file methods;
// the methods to access the structure of an attributes;  
 public:
  SgAttribute(int t, void *pt, int size, SgStatement &st;, int filenum);
  SgAttribute(int t, void *pt, int size, SgSymbol &st;, int filenum);
  SgAttribute(int t, void *pt, int size, SgExpression &st;, int filenum);
  SgAttribute(int t, void *pt, int size, SgType &st;, int filenum);
  ~SgAttribute();
  int getAttributeType();
  void setAttributeType(int t);
  void *getAttributeData();
  void *setAttributeData(void *d);
  int getAttributeSize();
  void setAttributeSize(int s);
  typenode getTypeNode();
  void *getPtToSage(); 
  void  setPtToSage(void *sa);
  void  resetPtToSage();
  void  setPtToSage(SgStatement &st;);
  void  setPtToSage(SgSymbol &st;);
  void  setPtToSage(SgExpression &st;);
  void  setPtToSage(SgType &st;);
  SgStatement *getStatement();
  SgExpression *getExpression();
  SgSymbol  *getSgSymbol();
  SgType  *getType();
  int getfileNumber();
  SgAttribute *copy(); 
  SgAttribute *getNext();
  void setNext(SgAttribute *s);
  int listLenght();
  SgAttribute *getInlist(int num);
  void save(FILE *file);
  void save(FILE *file, void (*savefunction)(void *dat,FILE *f));
```

`**SgAttribute**`**(int t, void *pt, int size, SgStatement &st;, int filenum)**

Конструктор для атрибута SgStatement. Параметр t - это тип атрибута, pt - указатель на данные, а size - размер данных (в байтах). Этот последний параметр полезен, если не задана функция для чтения и сохранения атрибутов. Параметр st - это оператор, к которому привязан атрибут. Когда атрибут создается таким образом, он не отображается в списке атрибутов узла SgStatement, но его можно добавить с помощью метода AddAttribute(SgAttribute *att).

`**SgAttribute**`**(int t, void *pt, int size, SgSymbol &st;, int filenum)**

Конструктор для атрибута SgSymbol.

`**SgAttribute**`**(int t, void *pt, int size, SgExpression &st;, int filenum)**

Конструктор для атрибута SgExpression.

`**SgAttribute**`**(int t, void *pt, int size, SgType &st;, int filenum)**

Конструктор для атрибута SgType.

`int **getAttributeType**`**()**

Получите тип атрибута.

`void **setAttributeType**`**(int t)**

Задайте тип атрибута.

`void ***getAttributeData**`**()**

Получаем поле данных атрибута.

`void ***setAttributeData**`**(void *d)**

Задайте поле данных для атрибута.

`int **getAttributeSize**`**()**

Возвращает размер поля данных атрибута.

`void **setAttributeSize**`**(int s)**

Задайте размер поля данных атрибута.

`typenode **getTypeNode**`**()**

Возвращает тип узла, к которому прикреплен атрибут. Этот тип является перечислимым:

    enum typenode {BIFNODE, LLNODE, SYMBNODE, TYPENODE,...} 

соответствует соответственно SgStatement, SgExpression, SgSymbol и SgType.

`void ***getPtToSage**`**()**

Возвращает указатель на узел sage, к которому привязан атрибут. Согласно getTypeNode(), это значение может быть приведено к нужному типу.

`void **setPtToSage**`**(void *sa)**

Установите указатель на узел Sage.

`void **resetPtToSage**`**()**

Установите для указателя на узел Sage значение NULL.

`void **setPtToSage**`**(SgStatement &st;)**

Установите указатель на узел Sage, а также на данные, к которым получает доступ функция getTypeNode().

`void **setPtToSage**`**(SgSymbol &st;)**

idem for Symbol.

`void **setPtToSage**`**(SgExpression &st;)**

idem for SgExpression.

`void **setPtToSage**`**(SgType &st;)**

idem for SgType.

`SgStatement ***getStatement**`**()**

Возвращает указатель SgStatement, если он существует и если атрибут привязан к узлу SgStatement. В противном случае эта функция возвращает значение NULL.

`SgExpression ***getExpression**`**()**

idem for SgExpression.

`SgSymbol ***getSgSymbol**`**()**

idem for Symbol.

`SgType ***getType**`**()**

idem for SgType.

`int **getfileNumber**`**()**

Возвращает номер файла.

`SgAttribute ***copy**`**()**

Получите копию атрибута. Эта функция не копирует поле данных.

`SgAttribute ***getNext**`**()**

Атрибуты, прикрепленные к одному и тому же узлу, объединяются в цепочку через следующее значение.

`void **setNext**`**(SgAttribute *s)**

Установите цепочку списков для атрибута.

#### Применение
С точки зрения пользователя, предпочтительным способом обработки атрибутов является использование атрибутивных методов классов SgStatement, SgExpression, SgSymbol и SgType. Класс SgAttribute предназначен для тех, кому нужна нестандартная функциональность. В частности, не следует напрямую использовать конструкторы SgAttribute. Вместо этого следует использовать методы AddAttribute и getAttribute. Например, у кого-то может возникнуть соблазн написать такой фрагмент кода, как этот:
```cpp
SgExpression * CurrentExpression;
     MyExprPtr = new MyExpr (  ...  );
     ...
     SgAttribute *MyAttribute = new SgAttribute ( MY_TYPE,
 (void *) MyExprPtr, sizeof(MyExpr) , *CurrentExpression , 0 );
 
     MyExprPtr->SetAttribute ( MyAttribute );
     CurrentExpression->addAttribute ( MyAttribute );
```
Вместо этого этот код должен быть записан следующим образом:
```cpp
     SgExpression * CurrentExpression;
     MyExprPtr = new MyExpr (  ...  );
     ...
     CurrentExpression->addAttribute ( MY_TYPE, (void *) MyExprPtr, sizeof(MyExpr) );

     MyAttribute =  CurrentExpression->getAttribute( 0, MY_TYPE )
     MyExprPtr->SetAttribute ( MyAttribute );
```

#### Примеры
Следующий фрагмент кода добавляет атрибут ко всем инструкциям всех файлов в проекте.
```cpp
            .....
    #define MY_ATTRIBUTE_TYPE 2
            .....
      nbfile = project->numberOfFiles();
      for (i=0; i< nbfile; i++)
        {
          file = &(project->file(i));
          first =   file->firstStatement();
          temp = first;
          while (temp)
            {
              str = new char[256];
              sprintf(str,"this_is_an_attribute_added_statement_line_%d",
                      temp->lineNumber());
              temp->addAttribute(MY_ATTRIBUTE_TYPE,(void *) str, strlen(str));
              temp = temp->lexNext();
            }
        }
```
Как извлечь атрибуты из списка инструкций.
```cpp
      for (i=0; i< nbfile; i++)
        {
          file = &(project->file(i));
          first =   file->firstStatement();
          temp = first;
          while (temp)
            {
              for (j=0; j< temp->numberOfAttributes(); j++)
                printf("Found attribute type %d ---> %s\n",
                       temp->attributeType(j),
                       (char *) temp->attributeValue(j));
              temp = temp->lexNext();
            }
        }
```
Как получить атрибуты непосредственно из файла:
```cpp
      SgFile *file;
      nba = file->numberOfAttributes();
      for (i=0 ; i< nba; i++)
        {
          att = file->attribute(i);
        }
```
Как сохранить атрибут:
```cpp
      for (i=0; i< nbfile; i++)
        {
          sprintf(nam,"attribute%d.dump",i);
          file = &(project->file(i));
          file->readAttributes(nam);
        }

```
Как сохранить с помощью пользовательской функции:
```cpp
    void  saveatt (void *dat,FILE *f)
    {
      if (!dat || !f)
        return;
      fprintf(f,"%s\n",dat);
    }
     ........

    for (i=0; i< nbfile; i++)
        {
          sprintf(nam,"attribute%d.dump",i);
          file = &(project->file(i));
          file->saveAttributes(nam,saveatt);
        }
```
Как читать с помощью пользовательской функции:
```cpp
    void  *readatt (FILE *f)
    {      
      char *data;
      if (!f)
        return NULL;
      data = new char[256];
      fscanf(f,"%s",data);
      return (void *) data;
    }
      ........

    for (i=0; i< nbfile; i++)
        {
          sprintf(nam,"attribute%d.dump",i);
          file = &(project->file(i));
          file->readAttributes(nam,readatt);
        }
```





