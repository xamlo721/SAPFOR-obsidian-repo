```cpp
// Instrumenting the entire program.

void FAnalyze(SgProject *project) {
  char s[32];

  printf ("Project has %d number of files\n", project->numberOfFiles());
  for (int i = 0; i < project->numberOfFiles(); i++) {
    SgFile *f;

    f = &(project->file(i));
    printf("Source file %s has", project->fileName(i));
    
    int num_routines;

    num_routines = f->numberOfFunctions();
    printf ("%d routines\n", num_routines);
    for (int j = 0; j < num_routines; j++) {
      SgStatement *sub;
      SgStatement *exe;
      
      sub = f->functions(j);
      exe = sub->lastDeclaration();
      InsertFCallNode(ENTRY_EVENT, exe, AFTER);
      FixLoops(sub);
//    FInstrumentSub(sub);
    }
    f->unparsestdout();
    printf ("\n Done unparsing\n");
  }

  for (i = 0; i < project->numberOfFiles(); i++) {
    SgFile *f;

    f = &(project->file(i));
    printf("Source file %s has", project->fileName(i));
    
    int num_routines;

    num_routines = f->numberOfFunctions();
    printf ("%d routines\n", num_routines);
    for (int j = 0; j < num_routines; j++) {
      SgStatement *sub;

      sub = f->functions(j);
      VistaInstrument(sub);
    }
    f->unparsestdout();
    printf ("\n Done unparsing\n");
  }

}
```