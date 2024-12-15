```cpp
// Looks into the expression for collection Array References
// Returns the type of the collection if it finds one.

SgDerivedCollectionType * isArrayRefOfCollection(SgExpression *expr) {
  SgType *type = NULL;
  SgExpression *lhs;
  SgVarRefExp *varef;
  SgDerivedCollectionType *dstype;
  
  if (!expr)
    return NULL;
  
  switch (expr->variant())
    {
    case FUNCTION_OP:
      lhs = expr->lhs();
      
      break;
    default :
      return NULL;
    }
  
  if (!lhs)
    return NULL;
  
  if (varef = isSgVarRefExp(lhs))
    {
      if (varef->symbol())
	type = varef->symbol()->type();
    }
  
  if (!type)
    return NULL;
  
  if (dstype = isSgDerivedCollectionType(type))
    return dstype;
  
  return NULL;
}
```