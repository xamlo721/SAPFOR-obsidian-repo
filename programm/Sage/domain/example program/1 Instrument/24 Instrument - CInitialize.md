```cpp
extern "C"
void CInitialize(SgProject *project) {
  CInitSymbols(project);
  InitFunctionTable(project);
}
```