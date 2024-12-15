```cpp
// given a type, traverse it and generate full infomration
void doFullType(SgType *t){
   SgArrayType *arrayt;
   SgPointerType *ptr;
   SgReferenceType *ref; // only for C++
   SgDerivedType *deriv;
   SgDescriptType *descr; // only for C and C++
   SgDerivedCollectionType *col; // only for pC++
   int i,n;

   if(arrayt = isSgArrayType(t)){
        printf("dimension("); 
	n = arrayt->dimension();
	for(i = 0; i < n; i++){
		(arrayt->sizeInDim(i))->unparsestdout();
		if(i < n-1) printf(", ");
		}
	printf(") ");
	}
   else{
	switch(t->variant()){
           case T_INT:     printf("integer "); break;
           case T_FLOAT:   printf("real "); break;
           case T_DOUBLE:  printf("double precision "); break;
           case T_CHAR:    printf("character "); break;
           case T_BOOL:    printf("boolean "); break;
           case T_STRING:  printf("string "); break;
           case T_RECORD:  printf("record.. more later "); break;
           case T_UNKNOWN: printf("unknown "); break;
           case T_COMPLEX: printf("complex "); break;
           case LOCAL:
           case INPUT: 
           case OUTPUT:
           case IO: 
               printf("do these later\n");
 	       break;
	   }
   }
   if(t->hasBaseType()){
	printf("of "); 
	doFullType(t->baseType());
	}
}
```