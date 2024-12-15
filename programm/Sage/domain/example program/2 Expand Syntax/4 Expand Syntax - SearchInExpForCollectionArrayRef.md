```cpp
// Need the level stuff to handle multiple references collection field
// references in one statement.

void SearchInExpForCollectionArrayRef(SgStatement *br, SgExpression *e,  int & level) {

  if (e == NULL)
    return;
  
  if (e->variant() == POINTST_OP) {
    
    SgDerivedCollectionType *a;
    SgSymbol *b;
	  
    a = isArrayRefOfCollection(e->lhs());
    b = isReferenceToElementField(e->rhs());
	  
    if (a && b) {
      ReplaceWithGetElemPart(br, e, a, b, level);
      level = level + 1;
    }
  }
  else {
    SearchInExpForCollectionArrayRef(br, e->lhs(), level);
    SearchInExpForCollectionArrayRef(br, e->rhs(), level);
  }
}
```