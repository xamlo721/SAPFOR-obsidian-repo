```cpp
// Initialize the function table (used for searching for functions).
void InitFunctionTable(SgProject *project) {

  int Files = project->numberOfFiles();
  int k = 0;

  for (int i = 0; i < project->numberOfFiles(); i++) {
    SgFile *f;
    
    f = &(project->file(i));
    
    int num_routines;
    
    num_routines = f->numberOfFunctions();
    for (int j = 0; j < num_routines; j++){
      SgStatement *sub;
      SgSymbol *subsym;

      sub = function_table[k].function = f->functions(j);
      subsym = sub->symbol();
      function_table[k++].function_name = subsym->identifier();
    }
  }

  totalfunctions = k;
}
```