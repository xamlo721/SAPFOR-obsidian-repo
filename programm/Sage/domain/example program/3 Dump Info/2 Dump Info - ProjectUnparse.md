```cpp
// the unparse operation regenerates source code.
// The function below prints the entire project to 
// stdout.  note:  the current unparser will only print
// to stdout.  in the near future we will have a version
// that will print to a string buffer.

void ProjectUnparse(SgProject *project) {
  for (int i = 0; i < project->numberOfFiles(); i++) {
    SgFile *f;
    
    f = &(project->file(i));
    f->unparsestdout();
  }
}
```