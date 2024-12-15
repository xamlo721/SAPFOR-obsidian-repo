```cpp  
// Fixing the loops in the subroutine (massaging the program)
void 
FixLoops(SgStatement* s)
{
  SgStatement *br;
  SgForStmt *f;

  for (br = s->lexNext(); ; br = br->lexNext()) {
    if (f = isSgForStmt(br))
      if (! f->isEnddoLoop())
	f->convertLoop();
   if (br == s->lastNodeOfStmt())
     break;
    
  }
}
```