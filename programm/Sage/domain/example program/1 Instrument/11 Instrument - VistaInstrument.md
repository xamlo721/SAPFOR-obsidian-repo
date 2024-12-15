```cpp
// needs to be filled in (used for instrumentation for animation)
void VistaInstrument(SgStatement *s) {
  SgStatement *br;
  SgExprListExp *l;
  SgExpression *e;
  SgExpression *a;

  for (br = s->lexNext(); ; br = br->lexNext()) {
    for (l = isSgExprListExp(br->expr(0)); l ; l = l->next()){
      e = l->value();
    }  
 
   if (br == s->lastNodeOfStmt())
     break;
  }  
}
```