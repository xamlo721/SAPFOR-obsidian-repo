```cpp
// print out the name and formal parameters for this subroutine,
// function or main program header.

void doRoutineHeader(SgStatement *s){
   SgProgHedrStmt *    prog;
   SgProcHedrStmt *    subr;
   SgFuncHedrStmt *    func;
   int i;
   SgSymbol *sy;

   if(subr = isSgProcHedrStmt (s)){
	printf("symbol:%s", (subr->name()).identifier());
        printf(" which is a suroutine.\n");
        printf("parameter list:\n");
	for(i = 0; i < subr->numberOfParameters(); i++){
		sy = subr->parameter(i);
		printf("parameter(%d):", i); doSymb(sy);
                printf(" of type: "); doFullType(sy->type());
		doSymbAttribs(sy); 
		printf("\n"); 
		}
	}
   else if(func = isSgFuncHedrStmt (s)){
	printf("symbol:%s", (func->name()).identifier());
        printf("which is a function of type ");
	doFullType((func->name()).type());
        printf("\n");
        printf("parameter list:\n");
	for(i = 0; i < func->numberOfParameters(); i++){
		sy = func->parameter(i);
		printf("parameter(%d):", i); doSymb(sy); 
                printf(" of type: "); doFullType(sy->type()); 
		doSymbAttribs(sy); 
		printf("\n"); 
		}
	}
}
```