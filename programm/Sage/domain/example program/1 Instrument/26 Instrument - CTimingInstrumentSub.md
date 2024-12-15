```cpp
// Instrument a pC++ function for timing collection invocations.

void CTimingInstrumentSub(SgStatement *s) {

  SgStatement *br;
  SgExprListExp *l;
  SgExpression *e;
  SgDerivedCollectionType *a;
  SgSymbol *b;

  for (br = s->lastDeclaration(); ; br = br->lexNext()) {
    for (l = isSgExprListExp(br->expr(0)); l ; l = l->next()){
      e = l->value();

      switch(e->variant()){
      case DEREF_OP:
      case POINTST_OP:
      case RECORD_REF:
	a = isReferenceToCollection(e, br);
	b = isReferenceToMethodOfElement(e->rhs());
	if (a && !b)
	  b = isReferenceToClassOfElement(a, e->rhs());

	if (a && isSgCExpStmt(br)) {
	  InsertCCallNode(TIMER_START, br, BEFORE);
	  InsertCCallNode(TIMER_STOP, br, AFTER);
          InsertCCallNode(TIMER_ELAPSED, br->lexNext(), AFTER);
	}
      }
    }
    if (br == s->lastNodeOfStmt())
      break;
  }
}
```