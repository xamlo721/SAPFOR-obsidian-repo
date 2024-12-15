Представляет собой подпрограммы Fortran.

```cpp
class  **SgProcHedrStmt**: public SgProgHedrStmt {
  // Fortran subroutine
  // variant == PROC_HEDR
public:        
  inline SgProcHedrStmt(int variant);
  inline SgProcHedrStmt(SgSymbol &name;, SgStatement &Body;);
  inline SgProcHedrStmt(SgSymbol &name;);
  inline SgProcHedrStmt(char *name);
  inline void AddArg(SgExpression &arg;); 
  SgExpression * AddArg(char *name, SgType &t;); // returns decl expr created.
  SgExpression * AddArg(char *name, SgType &t;, SgExpression &initializer;);
  inline int isRecursive();  // 1 if recursive.;
  inline int numberOfEntryPoints();      // the number of entry points
                                         // other than the main, 0 for C funcs.
  inline SgStatement *entryPoint(int i);  // the i-th entry point
  // this is incorrect. Takes only subroutines calls into account.
  // Should be modified to take function calls into account too.
  inline int numberOfCalls();            // number of calls to this proc.
  inline SgStatement *call(int i);       // position of the i-th call.  
  inline ~SgProcHedrStmt();
};      
```
#### Члены Класса 

`**SgProcHedrStmt**`**(int variant)**

document me

`**SgProcHedrStmt**`**(SgSymbol &name;, SgStatement Body)**

document me

`**SgProcHedrStmt**`**(SgSymbol &name;)**

document me

`**SgProcHedrStmt**`**(char *name)**

document me

`void **AddArg**`**(SgExpression &arg;)**

Этот метод используется для добавления формальных параметров в заголовок функции. Пожалуйста, смотрите подробное описание этого метода в разделе Указатели на функции.

`int **isRecursive**`**()**

document me

`int **numberOfEntryPoints**`**()**

document me

`SgStatement ***entryPoint**`**(int i)**

document me

`int **numberOfCalls**`**()**

document me

`SgStatement ***call**`**(int i)**

document me
#### Использование


#### Примеры
[[4 Dump Info - doRoutineHeader]]