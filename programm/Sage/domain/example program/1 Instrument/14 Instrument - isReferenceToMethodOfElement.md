```cpp
// Basic help routines (all obtained from the compiler)
// Should be made part of the library.
SgSymbol * isReferenceToMethodOfElement(SgExpression *expr) {
   SgVarRefExp *varef;
   SgFunctionCallExp *fcall;
   SgSymbol *symb;
   SgMemberFuncSymb *symbm;
   SgFieldSymb *symbf;
   if (!expr)
     return NULL;
   if (varef = isSgVarRefExp(expr)) {
       symb = varef->symbol();
   }
   if (fcall = isSgFunctionCallExp(expr)) {
       symb = fcall->symbol();
   }
   if (symbm = isSgMemberFuncSymb(symb)) {
       if (symbm->isMethodOfElement())
         return symbm;
       else
         return NULL;
   }
   if (symbf = isSgFieldSymb(symb)) {
       if (symbf->isMethodOfElement())
         return symbf;
       else
         return NULL;
   }
   return 0;
}
```