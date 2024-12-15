```cpp
void ReplaceWithGetElemPart(SgStatement *br, SgExpression *e, SgDerivedCollectionType *a, SgSymbol *b, int level) {

  SgBasicBlockStmt bgn;
  SgControlEndStmt nd;
  SgStatement *ext, *brnext;
  int matchingdummy;
  SgType *btype;
	    
  matchingdummy = MatchingDummyVar(a->elementClass());
  if (!matchingdummy)
    Message("Dummy variable has not been created!\n", 0);
	    
  br->insertStmtBefore(bgn, *(br->controlParent()));
  brnext = br->lexNext();
  ext = br->extractStmt();

  SgExpression dummy(RECORD_REF);
  dummy.setLhs(*DummyVarExpr[matchingdummy]);
  dummy.setRhs(*(e->rhs()));
	    
	    
  char addr1str[16], addr2str[16];
  if (level == 0) {
    strcpy(addr1str, "addr1");
    strcpy(addr2str, "addr2");
  }
  else {
    sprintf(addr1str, "addr1_%d", level);
    sprintf(addr2str, "addr2_%d", level);
  }

  SgPointerType p(*SgTypeInt());
  SgVariableSymb addr1(addr1str,p);
  SgVariableSymb addr2(addr2str,p);
  SgVarRefExp addr1ref(addr1), addr2ref(addr2);
	    
  
	    
  SgTypeArray *arrtype;
  if ((arrtype = isSgTypeArray(b->type())) && isSgArrayRefExp(e->rhs()))
    btype = arrtype->baseType();
  else
    btype = b->type();

  SgFunctionSymb *fsymb;

  if (btype->equivalentToType(*SgTypeInt()))
    fsymb = GetElemInt;
  else if (btype->equivalentToType(*SgTypeFloat()))
    fsymb = GetElemFloat;
  else if (btype->equivalentToType(*SgTypeDouble()))
    fsymb = GetElemDouble;
  else
    fsymb = GetElementPart;
	    
  SgFunctionCallExp func(*fsymb);		
  func.addArg(*(e->lhs()->rhs()));
  func.addArg(addr2ref - addr1ref);
	    
	    
// sizeof will be wrong for array's like x(i)->foo where foo
// is an array so do more work. Handle only one, two and three dimension
// cases.

// Need to work harder here. What about stuff like x(i)->foo[10] where the
// field foo is a 2d array.

  if ((arrtype = isSgTypeArray(b->type())) && isSgVarRefExp(e->rhs())) {
    if (arrtype->dimension() == 1)
      func.addArg(SgSizeOfOp(dummy) * arrtype->sizeInDim(0)->copy());
    else if (arrtype->dimension() == 2)
      func.addArg(SgSizeOfOp(dummy) * arrtype->sizeInDim(0)->copy()
		  * arrtype->sizeInDim(1)->copy());
    else if (arrtype->dimension() == 3)
      func.addArg(SgSizeOfOp(dummy) * arrtype->sizeInDim(0)->copy()
		  * arrtype->sizeInDim(1)->copy() 
		  * arrtype->sizeInDim(2)->copy());
  }
  else
    func.addArg(SgSizeOfOp(dummy));
  
  SgVarRefExp *collref;
  collref = isSgVarRefExp(e->lhs()->lhs()); 
  
  e->setVariant(RECORD_REF);
  e->setLhs(*collref);
  e->setRhs(func);
  
  
  SgExpression x1(ASSGN_OP);
  x1.setLhs(addr1ref);
  x1.setRhs(SgAddrOp(*DummyVarExpr[matchingdummy]));
  SgExprListExp exp1(x1);
  SgCExpStmt addr1assgn(exp1);
  
  SgExpression x2(ASSGN_OP);
  x2.setLhs(addr2ref);
  x2.setRhs(SgAddrOp(dummy));
  SgExprListExp exp2(x2);
  SgCExpStmt addr2assgn(exp2);
  
  bgn.insertStmtAfter(addr1assgn);
  addr1assgn.insertStmtAfter(addr2assgn);
  addr2assgn.insertStmtAfter(*ext);
  ext->insertStmtAfter(nd);
  
  addr1.declareTheSymbol(bgn);
  addr2.declareTheSymbol(bgn);
}
```