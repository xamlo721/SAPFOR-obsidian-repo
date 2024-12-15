```cpp
// Simple routines to look into a pC++ program.
void  ListCollections(SgFile *file) {
  SgStatement *s;
  SgCollectionStmt *c;

  for (s = file->firstStatement(); s ; s = s->lexNext()){
    if (c = isSgCollectionStmt(s)){
      c->unparsestdout();
    }
  }
}
```