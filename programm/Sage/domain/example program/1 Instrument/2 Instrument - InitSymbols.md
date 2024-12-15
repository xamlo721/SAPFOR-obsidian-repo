```cpp
// Initialize the function symbols (used in the instrumentation)
void  InitSymbols(SgProject *p) {
  SgFile *f;

  f = &(p->file(0));
  entry = new SgFunctionSymb(PROCEDURE_NAME,fnames[0],
			     *SgTypeInt(),*(f->firstStatement()));
  eexit  = new SgFunctionSymb(PROCEDURE_NAME,fnames[1],
			     *SgTypeInt(), *(f->firstStatement()));
  loop_entry= new SgFunctionSymb(PROCEDURE_NAME,fnames[2],
			      *SgTypeInt(), *(f->firstStatement()));
  loop_exit = new SgFunctionSymb(PROCEDURE_NAME,fnames[3],
			     *SgTypeInt(), *(f->firstStatement()));
}
```