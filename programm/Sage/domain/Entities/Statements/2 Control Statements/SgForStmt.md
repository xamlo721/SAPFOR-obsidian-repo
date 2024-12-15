Этот класс имеет набор высокоуровневых функций для семантического анализа и преобразований. Это включает в себя анализ неявных индукционных переменных, определенных в теле цикла, а также информацию о взаимодействиях с другими циклами, которые могут находиться в том же гнезде циклов. Кроме того, существуют функции для выполнения преобразований очень высокого уровня, таких как нормализация, взаимообмен, развертывание и объединение. Однако в текущей версии многие из этих функций по-прежнему не реализованы, поскольку они зависят от информации о зависимостях данных.

```cpp
class  **SgForStmt**: public SgStatement {
  // for Fortran Do and C for();
  // variant = FOR_NODE
public:
  inline SgForStmt(SgSymbol &do;_var, SgExpression &start;, SgExpression &end;,
            SgExpression &step;, SgStatement &body;);
  inline SgForStmt(SgSymbol *do_var, SgExpression *start, SgExpression *end,
            SgExpression *step, SgStatement *body);
  inline SgForStmt(SgSymbol &do;_var, SgExpression &start;, SgExpression &end;,
            SgStatement &body;);
  inline SgForStmt(SgExpression &start;, SgExpression &end;, SgExpression &step;,
            SgStatement &body;);
  
  inline SgSymbol * doName();                // the name of the loop (for F90.)
  inline void setDoName(SgSymbol &doName;);// sets the name of the loop(for F90)

  inline SgExpression *start();            
  inline void setStart(SgExpression &lbound;);

  inline SgExpression *end();
  inline void setEnd(SgExpression &ubound;);

  inline SgExpression *step();
  inline void setStep(SgExpression &step;);

  inline SgLabel *endOfLoop();

  // body is returned with control end statement
  //   still attached. 
  inline SgStatement *body();
  // s is assumed to terminate with a
  //   control end statement.
  inline void set_body(SgStatement &s;);
  inline int isPerfectLoopNest();
  inline SgStatement *getNextLoop(); 
  inline SgStatement *getPreviousLoop();   // returns outer nested loop
  inline SgStatement *getInnermostLoop();  // returns innermost nested loop
  inline int isEnddoLoop();            // TRUE if the loop ends with an Enddo
  inline int convertLoop();            // Convert the loop into a Good loop.
  inline ~SgForStmt();
};
```

#### Члены класса

`**SgForStmt**`**(SgSymbol &do;_var, SgExpression &start;, SgExpression &end;, SgExpression &step;, SgStatement &body;)**

document me

`**SgForStmt**`**(SgSymbol *do_var, SgExpression *start, SgExpression *end, SgExpression *step, SgStatement *body)**

document me

`**SgForStmt**`**(SgSymbol &do;_var, SgExpression &start;, SgExpression &end;, SgStatement &body;)**

document me

`**SgForStmt**`**(SgExpression &start;, SgExpression &end;, SgExpression &step;, SgStatement &body;)**

document me

`SgSymbol ***doName**`**()**

Returns the name of the loop for F90.

`void **setDoName**`**(SgSymbol &doName;)**

document me

`SgExpression ***start**`**()**

document me

`void **setStart**`**(SgExpression &lbound;)**

document me

`SgExpression ***end**`**()**

document me

`void **setEnd**`**(SgExpression &ubound;)**

document me

`SgExpression ***step**`**()**

document me

`void **setStep**`**(SgExpression &step;)**

document me

`SgLabel ***endOfLoop**`**()**

document me

`SgExpression &**bounds**`**()**

document me

`void **setBounds**`**(SgTripletOp &bounds;)**

document me

`SgStatement ***body**`**()**

Тело инструкции возвращается вместе с инструкцией with the control end

`void **set_body**`**(SgStatement &s;)**

document me

`int **isPerfectLoopNest**`**()**

document me

`SgStatement ***getNextLoop**`**()**

document me

`SgStatement ***getPreviousLoop**`**()**

document me

`SgStatement ***getInnermostLoop**`**()**

document me

`int **isEnddoLoop**`**()**

document me

`int **convertLoop**`**()**

document me

#### Примеры
[[2 Restructure - addStuffToProgram]]
[[5 Instrument - FixLoops]]
[[6 Dump Info - doLoopStmts]]
