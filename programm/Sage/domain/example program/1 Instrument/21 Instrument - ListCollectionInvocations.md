```cpp
void ListCollectionInvocations(SgFile *f) {
  SgStatement *br;
  SgExprListExp *l;
  SgExpression *e;
  SgStatement *s;
  SgDerivedCollectionType *a;
  SgSymbol *b;

  s = f->firstStatement();
  for (br = s; br; br = br->lexNext())
    for (l = isSgExprListExp(br->expr(0)); l ; l = l->next()){
      e = l->value();
      switch (e->variant()) {
        case DEREF_OP:
        case RECORD_REF:
        case POINTST_OP:
	  a = isReferenceToCollection(e, br);
	  b = isReferenceToMethodOfElement(e->rhs());
	  if (a && !b)
	    b = isReferenceToClassOfElement(a, e->rhs());
	  if (a && b)
	    br->unparsestdout();
      }
    }
}
```