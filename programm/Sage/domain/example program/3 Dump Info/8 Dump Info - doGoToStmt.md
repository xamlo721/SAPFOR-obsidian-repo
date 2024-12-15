```cpp
void doGoToStmt(SgStatement *s){
SgGotoStmt *   gotostmt;  
SgAssignedGotoStmt * assgoto;  
SgComputedGotoStmt * compgoto; 
  if(gotostmt = isSgGotoStmt(s)){
	printf("garden variety goto: branch to stmt with label [ %d ]\n",
		gotostmt->branchLabel()->id());

	}
  else if(assgoto = isSgAssignedGotoStmt(s)){}
  else if(compgoto = isSgComputedGotoStmt(s)){}
}
```