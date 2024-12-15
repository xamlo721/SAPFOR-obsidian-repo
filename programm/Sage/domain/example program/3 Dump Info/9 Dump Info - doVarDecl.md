```cpp
// this does variable declarations.
// there are lots of different forms that a
// declaration can take.  this just does the standard
// types now.  not done yet.

void doVarDecl(SgStatement *s){
SgVarDeclStmt * var;        
SgVarListDeclStmt *  varlist;   
SgStructureDeclStmt * strucdecl;   
SgNestedVarListDeclStmt*  declst; 
SgParameterStmt *    parm;    
SgImplicitStmt *     implic;   
   if (var = isSgVarDeclStmt(s)){
	 int i;
         printf("Variables declared here are:\n");
	 for(i = 0; i < var->numberOfSymbols(); i++){
		SgSymbol *s;
                s =  var->symbol(i);
                doSymb(s); printf(" of type: ");
		if(s->type()) doFullType(s->type());
		printf("\n");
		}
         } 
   else if (varlist = isSgVarListDeclStmt (s)){}
   /* else if (strucdecl = isSgStructureDeclStmt (s)){} */
   else if ( declst = isSgNestedVarListDeclStmt (s)){}
   else if ( parm = isSgParameterStmt (s)){}
   else if ( implic =  isSgImplicitStmt (s)){}
   else printf("not here!\n");
}
```