```cpp
int InDummyVarTable(SgType *x)  {

  for (int i=0; i < MAXDUMMYVAR; i++)
    if (DummyVarType[i] != NULL)
      if (DummyVarType[i]->equivalentToType(*x))
	return TRUE;

  return FALSE;
}
```