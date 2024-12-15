```cpp
  
//This main program assumes there is a fortran file called.
// x.f which has been parsed with cfp to generate a x.dep file.
// also there must be a project file x.proj  which
// is just one line containing the name x.dep
// multiple source files may be added to the project by adding
// the corresponding dep file name (one to a line.)
// however, sage has not been tested on multiple source
// files lately and it probably will not work.

int main(int argc, char **argv){

// better to grab the names from argv.
// but lets keep it simple.
  SgProject project("x.proj");
  SgFile file("x.f");
  int c;

// first check to see what language the source file is.
// each dep file has the language type encoded.

  switch (file.languageType()) {
	  case CSrc: // it is C or C++
	         printf("this is a c program.  this example is for fortran \n");
	    return -1;
	  case ForSrc: // it is a fortran 77 or fortran 90 program.
	      addStuffToProgram(&project;, &file;);
	      // ProjectUnparse(&project;);
	  }
  return 0;
}
```