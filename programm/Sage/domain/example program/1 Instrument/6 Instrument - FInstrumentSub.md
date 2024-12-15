```cpp
// Instrumentation running within a subroutine.
void 
FInstrumentSub(SgStatement* s)
{
  SgStatement *br;

  for (br = s->lexNext(); ; br = br->lexNext()) {
    switch (br->variant()){
    case FOR_NODE:
      InsertFCallNode(LOOP_ENTRY, br, BEFORE);
      InsertFCallNode(LOOP_EXIT, br->lastNodeOfStmt(), AFTER);
      break;
    default:
         break;
    }
    if (br == s->lastNodeOfStmt())
      break;
  }
}
```