```cpp  
int MatchingDummyVar(SgType *x) {
  for (int i=0; i < TotalDummyVars; i++)
    if (DummyVarType[i]->equivalentToType(*x))
      return i;
  return 0;
}
```