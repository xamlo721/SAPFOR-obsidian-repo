```cpp
void Init( SgFile *f) {
  char strin[256];
  SgStatement *fr;
  SgPointerType *p;
  SgSymbol *symb;

  fr = f->firstStatement();

  p = new SgPointerType(*SgTypeInt());
  GetElementPart = new SgFunctionSymb(FUNCTION_NAME, "Get_ElementPart", *p, *fr);
  GetElemInt = new SgFunctionSymb(FUNCTION_NAME, "Get_ElementPart_Int", *p, *fr);
  GetElemFloat = new SgFunctionSymb(FUNCTION_NAME, "Get_ElementPart_Float", *p, *fr);
  GetElemDouble = new SgFunctionSymb(FUNCTION_NAME, "Get_ElementPart_Double", *p, *fr);

  for (int i=0; i < MAXDUMMYVAR; i++)
    {
      DummyVar[i] = NULL;
      DummyVarType[i] = NULL;
      DummyVarExpr[i] = NULL;
    }

  SgType *type;
  SgDerivedCollectionType *ct;

  for (i=0,type = f->firstType(); type; type = type->next()) 
    {
      if (ct = isSgDerivedCollectionType(type))
	{
	  SgType *elementype;
	  elementype = ct->elementClass();
	  if (!InDummyVarTable(elementype))
	    {
	      SgClassStmt *fordef;

	      sprintf(strin, "Dummy_%d", i);
	      DummyVar[i] = new SgVariableSymb(strin, *elementype, *fr);
	      DummyVar[i]->declareTheSymbol(*fr);
	      DummyVarType[i] = elementype;
	      DummyVarExpr[i] = new SgVarRefExp(*DummyVar[i]);
	 
	      fordef = new SgClassStmt(*elementype->symbol());
	      fr->insertStmtAfter(*fordef);

	      i++;
	    }
      }
    }

  TotalDummyVars = i;
}
```