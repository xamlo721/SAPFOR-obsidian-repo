Представляет собой базовые блоки языка Си.

```cpp
class **SgBasicBlockStmt**: public SgStatement {
  // in C we have: {  body; }
  // variant == BASIC_BLOCK
public:
  inline SgBasicBlockStmt();
  inline ~SgBasicBlockStmt();
};
```

#### Использование

Не все операторы, которые являются составными в C и C++, представлены в виде SgBasicBlockStmt. Те, которые не являются составными, включают в себя: тела функций, ветви операторов if, тела операторов while и т.д. Только те составные операторы, которые не попадают в вышеуказанную категорию, представлены как SgBasicBlockStmt. Например:

```cpp
while(1){
  int i;
  i = 0;
}
```
не содержит SgBasicBlockStmt, в то время как,
```cpp
void foo(){
  int i; 
  {
    int j;
    j = 0;
  }
  i = 1;
}
```
включает в себя один SgBasicBlockStmt.

#### Примеры
[[5 Expand Syntax - ReplaceWithGetElemPart]]