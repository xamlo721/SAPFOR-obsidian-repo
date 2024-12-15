```cpp
// Basic initialization
extern "C"
void
FInitialize(SgProject *project)
{
  InitSymbols(project);
  InitFunctionTable(project);
}
```