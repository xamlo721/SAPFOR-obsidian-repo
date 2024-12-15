```cpp
//
// where is used to disambiguate this
//
SgDerivedCollectionType * isReferenceToCollection(SgExpression *expr, SgStatement *where) {
   SgType *type = NULL;
   SgExpression *lhs;
   SgVarRefExp *varef;
   SgPointerType *tpt;
   SgReferenceType *tref;
   SgDerivedCollectionType *dstype;
   SgArrayRefExp *array;
   SgSymbol *symb;
   SgFunctionCallExp *func;

   if (!expr)
     return NULL;
   switch (expr->variant())
     {
     case RECORD_REF:
     case POINTST_OP:
     case DEREF_OP:
       lhs = expr->lhs();
       break;
     case VAR_REF:
     case ARRAY_REF:
     case FUNC_CALL:
       lhs = expr;
       break;
       default :
// default should be to try to generate a copy for the expression
// and see if expression becomes call the function again.
         return NULL;
     }
   if (!lhs)
     return NULL;
   if (varef = isSgVarRefExp(lhs))
     {
       if (varef->symbol())
         type = varef->symbol()->type();
     } else
       if (isSgThisExp(lhs))
         {
           if (inMethodOfTheElement(where))
             return 0; // this refer to the element 
           type = lhs->type();
         } else
           if (array = isSgArrayRefExp(lhs))
             {
               symb = array->symbol();
               if (symb)
                 type = symb->type();
               if (type)
                 type = type->internalBaseType();
             } else  
               if (func = isSgFunctionCallExp(lhs))
                 {
                   symb = func->symbol();
                   if (symb)
                     type = symb->type();
                 } else
                   if  (isSgPointerDerefExp(lhs))
                     {
                       type = isReferenceToCollection(lhs,where);
                     } else
                       if  (isSgExprListExp(lhs))
                         {
                           type = isReferenceToCollection(lhs->lhs(),where);
                         } else
                           return NULL;
   if (!type)
     return NULL;
   switch (expr->variant())
     {
     case FUNC_CALL:
     case ARRAY_REF:
     case VAR_REF:
     case RECORD_REF:
       if (dstype = isSgDerivedCollectionType(type))
         return dstype;
       if (tref = isSgReferenceType(type))
         {
           type = tref->baseType();
           if (dstype = isSgDerivedCollectionType(type))
             return dstype;
         }
       break;
     case DEREF_OP:
     case POINTST_OP: 
       if (tpt = isSgPointerType(type))
         {
           type = tpt->baseType();
           if (dstype = isSgDerivedCollectionType(type))
             return dstype;
           if (tref = isSgReferenceType(type))
             {
               type = tref->baseType();
               if (dstype = isSgDerivedCollectionType(type))
                 return dstype;
             }
         }
       break;
     }
   return NULL;
 }
```