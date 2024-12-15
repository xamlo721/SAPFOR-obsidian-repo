```cpp
extern "C"
void UnparseSub(char *name) {
  SgStatement *sub;

  for(int i=0; i < totalfunctions; i++) {
    if (strcmp(name, function_table[i].function_name) == 0)
      break;
  }

  sub = function_table[i].function;
  sub->unparsestdout();
}
```