```cpp
// Instrumentation based on function name.

extern "C"
void CTimingInstrument(char *name) {

  for(int i=0; i < totalfunctions; i++) {
    if (strcmp(name, function_table[i].function_name) == 0)
      break;
  }

  CTimingInstrumentSub(function_table[i].function);
}
```