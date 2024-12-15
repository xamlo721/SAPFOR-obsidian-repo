Представляет операторы данных блока Fortran.

```cpp
class  **SgBlockDataStmt**: public SgStatement {
  // Fortran Block Data statement
  // variant == BLOCK_DATA
public:
  SgBlockDataStmt(SgSymbol &name;, SgStatement &body;);
  ~SgBlockDataStmt();
  
  SgSymbol *name();  // block data name if given;
  int setName(SgSymbol &symbol;);           // set block data name 
  
  int isSymbolInScope(SgSymbol &symbol;);
  int isSymbolDeclaredHere(SgSymbol &symbol;);
};
```
#### Члены класса
`**SgBlockDataStmt**`**(SgSymbol &name;, SgStatement &body;)**

document me

`SgSymbol ***name**`**()**

document me

`int **setName**`**(SgSymbol &symbol;)**

document me

`int **isSymbolInScope**`**(SgSymbol &symbol;)**

document me

`int **isSymbolDeclaredHere**`**(SgSymbol &symbol;)**

document me

