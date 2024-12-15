```cpp
void CAnalyze(SgProject *project){

  for (int i = 0; i < project->numberOfFiles(); i++) {
    SgFile *f;
    
    f = &(project->file(i));
    ListCollections(f);
    ListCollectionInstances(f);
    printf("Source file %s has ", project->fileName(i));
    
    int num_routines;
    
    num_routines = f->numberOfFunctions();
    printf ("%d routines\n", num_routines);
    ListCollectionInvocations(f);
  }
}
```