```cpp
void ExpandSyntax(SgFile *f) {
  SgStatement *br;
  SgExprListExp *l;
  SgExpression *e;
  SgStatement *s;
  int lvl = 0;

  s = f->firstStatement();
  for (br = s; br; br = br->lexNext()) 
    if (isSgCExpStmt(br)) {
      for (l = isSgExprListExp(br->expr(0)); l ; l = l->next()) {
	e = l->value();
	SearchInExpForCollectionArrayRef(br,e, lvl);	
	lvl = 0;
      }
    }
}
```