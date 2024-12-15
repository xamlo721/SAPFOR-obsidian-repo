```cpp  
main(int argc, char **argv){

  SgProject project("simple.proj");
  SgFile file("simple.pc");
  int c;

  switch (file.languageType()) {
  case CSrc:
    
#if 1
    CAnalyze(&project;);
    ProjectUnparse(&project;);
#endif
    break;

  case ForSrc:
    printf("Wrong language!\n");
    exit(-1);
  }
}
```