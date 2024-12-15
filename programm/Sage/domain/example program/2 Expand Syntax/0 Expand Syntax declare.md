```cpp
/*********************************************************************/
/*                  pC++/Sage++  Copyright (C) 1993                  */
/*  Indiana University  University of Oregon  University of Rennes   */
/*********************************************************************/

/******************************************************************
**  A Simple application of Sage++ that analyzes pC++ programs and does
**  one simple source transformation to eliminate some extra communication
**  and expand some syntax.
**  
**  pC++ has distributed data-structures called Collections that are
**  homogenous and they contain classes as elements. In a pC++ program to
**  refer to any particular element an array like syntax is used. To refer
**  to a field within an element that resides on someother processor is
**  expensive at present. The reason being when a reference to a nonlocal
**  element occurs the whole element is brought in and then the particular
**  field that is required is extracted from it.
**  
**  This application analyzes pC++ program for "Collection Array
**  References" and transforms them so that the communication for getting
**  fields of non local elements is not more than the "length" of the
**  field.
**  
**  As an example consider the following pC++ program and in
**  Processor_Main are some potential non local references.
**  
**  class Simple{
**   public:
**    int foo;
**    float bar[10];
**    void hello() {printf("hello world\n");};
**  };
**  
**  #include "distarray.h"
**  
**  Collection DistBlkVector: SuperKernel
**  {
**   public:
**    DistBlkVector(Distribution *T, Align *A);
**   MethodOfElement:
**    virtual void hello();
**  };
**  
**  
**  DistBlkVector::DistBlkVector(Template *T, Align *A):SuperKernel(T, A)
**  {}
**  
**  
**  void Processor_Main()
**  {
**    int i,j;
**    Processors P;
**    Distribution T(GRIDSIZE,&P;,BLOCK);
**    Align  A(GRIDSIZE,"[ALIGN(V[i],T[i])]");
**    Distribution T1(GRIDSIZE,GRIDSIZE&P;,BLOCK, BLOCK);
**    Align A1(GRIDSIZE,"[ALIGN(V[i][j],T[i][j])]");
**    DistBlkVector<Simple>   x(&T;,&A;);
**    DistBlkVector<Simple>   y(&T;,&A;);
**
**    x(i)->foo; // xformed to x.Get_ElementPart_Int(i, <foo-offset>, <sizeof (int)>)
**    x(i)->hello();
**  
**    y(i,j)->bar // xformed to y.GetElementPart(i, <bar-offset>, 10 * <sizeof (float)>)
**    y(i,j)->hello();
**  
**  }
**  
*****************************************************************/

#include <stdio.h>
#include <malloc.h>
#include <sage++user.h>

// Make the dummy var table into a class and clean it up.
#define MAXDUMMYVAR 20

SgSymbol     *DummyVar[MAXDUMMYVAR];
SgType       *DummyVarType[MAXDUMMYVAR];
SgExpression *DummyVarExpr[MAXDUMMYVAR];

int TotalDummyVars = 0;

SgFunctionSymb *GetElementPart, *GetElemInt, *GetElemFloat, *GetElemDouble;
SgVariableSymb *addr1, *addr2;

void SearchInExpForCollectionArrayRef(SgStatement *br, SgExpression *e, 
				      int & level);
void ReplaceWithGetElemPart(SgStatement *br, SgExpression *e, 
			    SgDerivedCollectionType *a, SgSymbol *b, int level);
int MatchingDummyVar(SgType *x);
```

[[1 Expand Syntax - isReferenceToElementField]]
[[2 Expand Syntax - isArrayRefOfCollection]]
[[3 Expand Syntax - ExpandSyntax]]
[[4 Expand Syntax - SearchInExpForCollectionArrayRef]]
[[5 Expand Syntax - ReplaceWithGetElemPart]]
[[6 Expand Syntax - MatchingDummyVar]]
[[7 Expand Syntax - InDummyVarTable]]
[[8 Expand Syntax - Init]]
[[9 Expand Syntax - CAnalyze]]
[[10 Expand Syntax - ProjectUnparse]]
[[11 Expand Syntax - main]]


