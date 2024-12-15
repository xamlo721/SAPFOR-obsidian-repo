```cpp
// Instrumentation call (search for function symbol based on function name)
extern "C"
void
FInstrument(char *name)
{
  SgStatement *sub;

  for(int i=0; i < totalfunctions; i++) {
    if (strcmp(name, function_table[i].function_name) == 0)
      break;
  }

  sub = function_table[i].function;
  FixLoops(sub);
  InsertFCallNode(ENTRY_EVENT, sub->lastDeclaration(), AFTER);
  InsertFCallNode(EXIT_EVENT, sub->lastExecutable(), AFTER);
  FInstrumentSub(function_table[i].function);
}
```