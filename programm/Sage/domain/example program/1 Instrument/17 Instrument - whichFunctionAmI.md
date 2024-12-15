```cpp
SgFuncHedrStmt * whichFunctionAmI(SgStatement *where) {
  SgFuncHedrStmt *fh;
  SgMemberFuncSymb *symb;

  if (!where)
    return NULL;

  if (where->variant() == GLOBAL)
    return NULL;

  if (fh = isSgFuncHedrStmt(where)) {
      return fh;
  }
  return whichFunctionAmI(where->controlParent());
}
```