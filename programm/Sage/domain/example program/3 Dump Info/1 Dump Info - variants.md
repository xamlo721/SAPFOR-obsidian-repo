```cpp
// each object in the .dep file has an integer "variant" to // describe its type. There is a standard defined name for // each and that may be retrieved from the array "tag" below. 
#define MAXTAGS 1000 
static char *tag[MAXTAGS]; 
void initVariantNames(){ 
	for(int i = 0; i < MAXTAGS; i++) 
		tag[i] = NULL; 
	#include "../h/tag.h" 
} 

void printVariantName(int i){ 

	if((i >= 0 && i < MAXTAGS) && tag[i]) 
		printf("%s", tag[i]); 
	else 
		printf("not a known node variant"); 
}
```