```cpp
// Insert a C function call statement
void InsertCCallNode(int event_type, SgStatement *s, int how) {
  SgSymbol *symb;
       
  switch (event_type) {
    case TIMER_CLEAR: symb = timer_clear;
                      break;
    case TIMER_START: symb = timer_start;
                      break;
    case TIMER_STOP:  symb = timer_stop;
                      break;
    case TIMER_ELAPSED: symb = timer_elapsed;
                       break;
  }

  SgFunctionCallExp *func;
  SgExprListExp *exp;
  SgCExpStmt *c;

  func = new SgFunctionCallExp(*symb);
  exp = new SgExprListExp();
  exp->setValue(*func);
  c = new SgCExpStmt (*exp);

  switch (how) {
    case BEFORE: 
         s->insertStmtBefore(*c);
         break;
    case AFTER:
         s->insertStmtAfter(*c);
         break;
  }
}
```