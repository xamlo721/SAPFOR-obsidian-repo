```cpp
void classifySymbols(SgFile *f){ 
	SgSymbol *s; 
	SgVariableSymb *vs; 
	SgConstantSymb *cs; 
	SgFunctionSymb *fs; 
	SgLabelVarSymb *lvs; 
	SgExternalSymb *exts; 
	SgConstructSymb *cnsts; 
	SgInterfaceSymb *ifs; 
	SgModuleSymb *mods; 

	for(s = f->firstSymbol(); s; s = s->next()) { 
		printf("SYMB[%d]: %s = %s scope=STMT[%d] type:", 
			s->id(),
			tag[s->variant()], 
			s->identifier(), 
			(s->scope())?(s->scope())->id(): -1); 
		
		if(s->type()) doFullType(s->type()); 
		
		doSymbAttribs(s); 
		printf("\n"); 
		switch(s->variant()){ 
			case CONST_NAME: 
			case VARIABLE_NAME: 
			case PROGRAM_NAME: 
			case PROCEDURE_NAME: 
			case LABEL_VAR: /* dest of assigned goto stmt */ 
			case FUNCTION_NAME: 
			case LABEL_NAME: /* new added for VPC */ 
			case ROUTINE_NAME: /*added for external statement*/ 
			case CONSTRUCT_NAME: 
			case INTERFACE_NAME: 
			case MODULE_NAME: 
				printf(" need work\n"); 
				break; 
			default: 
				printf("forgot one\n"); 
				break; 
		} 
	} 
}
```
