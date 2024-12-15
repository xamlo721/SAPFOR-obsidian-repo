```cpp
SgSymbol *isReferenceToClassOfElement(SgDerivedCollectionType *type,SgExpression *expr) {
  SgVarRefExp *varef;
  SgFunctionCallExp *fcall;
  SgSymbol *symb,*elsymb;
  SgMemberFuncSymb *symbm;
  SgFieldSymb *symbf;
  SgType *elmetype;
  SgDerivedType *eltype;

   if (!expr || !type)
     return NULL;
  elmetype = type->elementClass();
  if (!elmetype)
    return NULL;
  if (elmetype->isTheElementType())
    return NULL;
  
  if (eltype = isSgDerivedType(elmetype)) {
      if (!(elsymb = eltype->typeName())) {
          return NULL;
        }
  } else
      return NULL;

   if (varef = isSgVarRefExp(expr)) {
       symb = varef->symbol();
   }
   if (fcall = isSgFunctionCallExp(expr)) {
       symb = fcall->symbol();
   }

   if (symbm = isSgMemberFuncSymb(symb)) {
       if (symbm->className() == elsymb)
         return symbm;
       else
         return NULL;
   }
   if (symbf = isSgFieldSymb(symb)) {
       if (symbf->structureName() == elsymb)
         return symbf;
       else
         return NULL;
   }
   return NULL;
}
```