```cpp
// this routine handles the different types of "if" statements.
// not finished.
void doIfStmts(SgStatement *s){
SgLogIfStmt *    logif;   
SgIfStmt *       ifst;        
SgArithIfStmt *  arithif;  

   if (logif = isSgLogIfStmt (s)){
	printf("logical if: condition EXPR[%d] ", logif->conditional()->id());
	(logif->conditional())->unparsestdout();
	printf(" :if true do STMT[%d]\n", (logif->body())->id());
	}
   else if(ifst = isSgIfStmt (s)){}
   else if(arithif = isSgArithIfStmt (s)){}
}
```