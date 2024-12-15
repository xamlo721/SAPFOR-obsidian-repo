```cpp 
SgSymbol * isReferenceToElementField(SgExpression *expr) {
  SgVarRefExp *varef;
  SgArrayRefExp *aref;
  SgSymbol *symb;
  SgFieldSymb *symbf;

  if (!expr)
    return NULL;
  if (varef = isSgVarRefExp(expr))
    {
      symb = varef->symbol();
      if (symbf = isSgFieldSymb(symb))
	return symbf;
    }
  else if (aref = isSgArrayRefExp(expr))
    {
      symb = aref->symbol();
      if (symbf = isSgFieldSymb(symb))
	return symbf;
    }
  return NULL;
}
```