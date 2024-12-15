```cpp
// Initializing the timer function symbols.
void CInitSymbols(SgProject *p) {
  SgFile *f;

  f = &(p->file(0));
  timer_clear = new SgFunctionSymb(FUNCTION_NAME,cnames[0],
				   *SgTypeInt(),*(f->firstStatement()));
  timer_start  = new SgFunctionSymb(FUNCTION_NAME,cnames[1],
				    *SgTypeInt(), *(f->firstStatement()));
  timer_stop = new SgFunctionSymb(FUNCTION_NAME,cnames[2],
				  *SgTypeInt(), *(f->firstStatement()));
  timer_elapsed = new SgFunctionSymb(FUNCTION_NAME,cnames[3],
				     *SgTypeInt(), *(f->firstStatement()));
}
```