```cpp
int inMethodOfTheElement(SgStatement *where) {
  SgFuncHedrStmt *fh;
  SgMemberFuncSymb *symb;

  if (!where)
    return 0;

  if (where->variant() == GLOBAL)
    return 0;

  if (fh = isSgFuncHedrStmt(where)) {
      if (symb = isSgMemberFuncSymb(fh->symbol())) {
          return symb->isMethodOfElement();
        }
    }
  return inMethodOfTheElement(where->controlParent());
}
```