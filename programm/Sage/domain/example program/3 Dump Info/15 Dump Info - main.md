```cpp
int main(int argc, char **argv){

  SgProject project("x.proj");
  SgFile file("x.f");
  int c;

  initVariantNames();

  switch (file.languageType()) {
	  case CSrc:
	         printf("this is a c program.  this example is for fortran \n");
	         return -1;
	  case ForSrc:
	         classifyStatements(&file;);
	         printf("**************************************************\n");
	         printf("**** Expression Table ****************************\n");
	         printf("**************************************************\n");
	         classifyExpressions(&file;);
	         printf("**************************************************\n");
	         printf("**** Symbol  Table *******************************\n");
	         printf("**************************************************\n");
	         classifySymbols(&file;);
	  }
  return 0;
}
```