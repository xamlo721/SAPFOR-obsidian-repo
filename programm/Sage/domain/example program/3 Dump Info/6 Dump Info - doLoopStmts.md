```cpp
// this routine handles the different types of loop statements.
// only does do loops now.  more later.

void doLoopStmts(SgStatement *s){
SgForStmt *  doloop;    
SgWhileStmt *  whileloop;          
SgExpression *e;
   if (doloop = isSgForStmt(s)){
	printf("a DO LOOP: control var:");
	doSymb(doloop->symbol());
	printf("\n lower bound = ");
	if(e = doloop->start()) e->unparsestdout();
	printf("  , upper bound = ");
	if(e = doloop->end()) e->unparsestdout();
	if(e = doloop->step()){
		printf(" , step = ");
	 	e->unparsestdout();
		}
	printf(" \n");
	if(doloop->endOfLoop()){
		printf("end of loop label[%d]\n",(doloop->endOfLoop())->id());
		}
	}
   else if(whileloop = isSgWhileStmt (s)){}
   else printf("not finished\n");
}
```