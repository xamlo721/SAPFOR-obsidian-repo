```cpp
void ProjectUnparse(SgProject *project) { 
	for (int i = 0; i < project->numberOfFiles(); i++) { 
		SgFile *f; 
		f = &(project->file(i)); 
		f->unparsestdout(); 
	} 
}
```