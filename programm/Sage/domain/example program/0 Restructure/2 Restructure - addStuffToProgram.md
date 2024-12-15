```cpp
void addStuffToProgram( SgProject *project, SgFile *file){
  SgValueExp c1(1), c2(2), c3(3), c100(100);
  SgExpression *pt;
  SgVarRefExp  *e1, *e2, *e3, *e4;
  SgStatement *themain, *first, *firstex, *last;
  SgFuncHedrStmt *ptfunc;
  SgSymbol *ptsymb;
  SgSymbol *i1;
  SgSymbol *i2;
  SgSymbol *i3;
  SgSymbol *i4;
  SgSymbol *anarray;
  SgAssignStmt *stmt, *stmt1;
  SgIfStmt *anif;
  SgStatement *anotherif;
  SgWhileStmt *awhile;
  SgForStmt *afor;
  SgReturnStmt *areturn;
  SgCallStmt *afuncall;
  SgArrayType *typearray;
  SgType basetype(T_FLOAT);

  printf("There is %d files in that project\n",project->numberOfFiles());

  // get the first statement in the file this is the GLOBAL_BFND, i.e.
  // the header for the file and not a real statement in the program.

  first = (file->firstStatement());
  // find the main program.
  themain = (file->mainProgram());
  if(!themain){
           printf("no main program here!\n");
           return;
	   }

  // first create a new function 

  ptfunc = new SgFuncHedrStmt("funct1");

  // next add some parameters.

  ptsymb = new SgVariableSymb("var1");
  pt = new SgVarRefExp(*ptsymb);
  ptfunc->AddArg(*pt);

  ptsymb = new SgVariableSymb("var2");
  pt = new SgVarRefExp(*ptsymb);
  ptfunc->AddArg(*pt);

  // Now insert our function after the file
  // header. this is a bit hard to read. 
  // x->instertStmtAfter(y) means put y after x.

  first->insertStmtAfter(*ptfunc);

  // lets add a statement to that function 
  // first declare some integer variables.

  i1 = new SgVariableSymb("i1");
  i1->declareTheSymbol(*ptfunc);
  e1 = new SgVarRefExp(*i1);

  i2 = new SgVariableSymb("i2");
  i2->declareTheSymbol(*ptfunc);
  e2 = new SgVarRefExp(*i2);

  i3 = new SgVariableSymb("i3");
  i3->declareTheSymbol(*ptfunc);
  e3 = new SgVarRefExp(*i3);
  
  i4 = new SgVariableSymb("i4");
  i4->declareTheSymbol(*ptfunc);
  e4 = new SgVarRefExp(*i4);

  // next find the last declaration in the function.
  // so that we can add statements after it.

  firstex = (ptfunc->lastDeclaration());

  // make the assignment i1 = i2 + (i3 + 1)*i4

  stmt = new SgAssignStmt((*e1), (*e2) + ((*e3) + c1) * (*e4));

  // mane another assignment i2 = i3

  stmt1 = new SgAssignStmt(*e2,*e3);

  // make an if statement: if( 1.gt.2) then
  //                          stmt1
  //                       else 
  //                          a copy of stmt
  //                       endif

  anif = new SgIfStmt(c1 > c2 , *stmt1, stmt->copy());

  // make another if statement that is a copy of the last.

  anotherif = &(anif->copy());
  
  // make a while loop: while (i4 < 2) 
  //                         a copy of the if statement
  //                    endwhile

  awhile = new SgWhileStmt( (*e4)< c2 , anif->copy());

  // make a do loop:  do i1 = 1, 2, 3
  //                      a copy of the while statement
  //                  enddo

  afor = new SgForStmt(* i1, c1, c2, c3, awhile->copy());

  // now a return statement

  areturn = new SgReturnStmt();

  // now a subroutine call:  call funct1(1,2,3) 

  afuncall = new SgCallStmt(*ptfunc->symbol());
  afuncall->addArg(c1.copy());
  afuncall->addArg(c2.copy());
  afuncall->addArg(c3.copy());
  
// let insert what we have created into the subroutine.
// note these will come out in reverse order of insertion
// becuase we keep inserting them after the last declaration.

  firstex->insertStmtAfter(*anif);
  firstex->insertStmtAfter(stmt->copy());
  firstex->insertStmtAfter(*awhile);
  firstex->insertStmtAfter(*afor);

// to do it the other way, find the last statement.
// and insert the return at the end.

  last = (ptfunc->lastExecutable());
  last->insertStmtAfter(*areturn);

// now put the if and the function call in the main
// program.
  
  themain->insertStmtAfter(*anotherif);
  themain->insertStmtAfter(*afuncall);

// Let's create an array.  basetype was declared as float above.
// first we create a type.  in sage an array type is its base
// type plus its dimensions (ranges).

   typearray = new SgArrayType(basetype);
   typearray->addRange(c1);
   typearray->addRange(c2);
   typearray->addRange(c3);
  
// now create the array symbol of this type.

   anarray = new SgVariableSymb("Array1",*typearray);
   anarray->declareTheSymbol(*ptfunc);

// make an array expression Array1(i1, i2, i3)

   pt =  new SgArrayRefExp(*anarray,*e1,*e2,*e3);

// make an assignment statement 
//   Array1(i1, i2, i3) = i2 + (Array1(i1,i2,i3) + 1)*Array1(i1,i2,i3)

   stmt = new SgAssignStmt((*pt), (*e2) + ((*pt) + c1) * (*pt));

// insert it into our subroutine.

   firstex->insertStmtAfter(*stmt);

// unparse the file
  file->unparsestdout();

// and save the modified dep file.

  file->saveDepFile("debug.dep");
  
}
```