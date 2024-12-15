```cpp
// Inserting a call to the instrumentation library
void InsertFCallNode(int event_type, SgStatement *s, int how)
{
  SgSymbol *symb;
       
  switch (event_type) {
    case ENTRY_EVENT: symb = entry;
                    break;
    case EXIT_EVENT:  symb = eexit;
                    break;
    case LOOP_ENTRY:  symb = loop_entry;
                    break;
    case LOOP_EXIT :  symb = loop_exit;
                    break;
  }

  SgCallStmt *c;
  SgValueExp *ev;

  c = new SgCallStmt(*symb);
  ev = new SgValueExp(event);
  c->addArg(*ev);
  delete(ev);

  event++;

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