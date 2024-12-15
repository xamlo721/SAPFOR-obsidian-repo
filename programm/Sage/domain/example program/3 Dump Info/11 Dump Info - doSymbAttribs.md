```cpp
void doSymbAttribs(SgSymbol *s){ 
int i; 
if(s->attributes()) { 
	i = s->attributes(); 
	printf(" attributes =( "); 
	if(i & ALLOCATABLE_BIT ) { printf(" allocatable,"); } 
	if(i & DIMENSION_BIT ){  printf(" dim,");  } 
	if(i & EXTERNAL_BIT ){  printf(" extern,");  } 
	if(i & IN_BIT ){ printf(" in,"); } 
	if(i & INOUT_BIT ){ printf(" inout,"); } 
	if(i & INTRINSIC_BIT ){ printf(" intrinsic,"); } 
	if(i & OPTIONAL_BIT ){ printf(" optional,"); } 
	if(i & OUT_BIT ){ printf(" out,"); } 
	if(i & PARAMETER_BIT ){ printf(" parameter,"); } 
	if(i & POINTER_BIT ){ printf(" pointer,"); } 
	if(i & PRIVATE_BIT ){ printf(" private,"); } 
	if(i & PUBLIC_BIT ){ printf(" public,"); } 
	if(i & SAVE_BIT ){ printf(" save,"); } 
	if(i & SEQUENCE_BIT ){ printf(" seq,"); } 
	if(i & RECURSIVE_BIT ){ printf(" recur,"); } 
	if(i & TARGET_BIT ){ printf(" target,"); } 
	printf(")"); } }
```