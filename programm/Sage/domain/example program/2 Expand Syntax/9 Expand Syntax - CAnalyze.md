```cpp
void CAnalyze(SgProject * project){

  for (int i = 0; i < project->numberOfFiles(); i++) {
    SgFile *f;

    
    f = &(project->file(i));
    Init(f);
    ExpandSyntax(f);
  }
}
```