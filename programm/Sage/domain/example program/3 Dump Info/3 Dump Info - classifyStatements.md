```cpp
  
// some forward declarations.

void doExpr(SgExpression *e);
void doSymb(SgSymbol *s);
void doType(SgType *t);
void doRoutineHeader(SgStatement *s);
void doIfStmts(SgStatement *s);
void doLoopStmts(SgStatement *s);
void doIOStmts(SgStatement *s);
void doGoToStmt(SgStatement *s);
void doVarDecl(SgStatement *s);
void doFullType(SgType *t);
void doSymbAttribs(SgSymbol *s);

// this function traverses the list of statements in a file.
// for each statement it prints out all the information available
// in the .dep data base.

void classifyStatements(SgFile *f){
  SgStatement *line;
  SgStatement *s;
  int i,j;

  // grab the first statement in the file.
  s = f->firstStatement();

  // follow the statements in lexical order.
  // an alternative is to follow them in scope order
  // using a recursive traversal, but this is simpler
  // for what we want to do here.

  for (line = s; line; line = line->lexNext()){
   printf("---------------------------------------------------------------------\n");
         // print the line to the standard out.
         // note: if the statement controls other blocks
         // nested within, it will print the entire block
         // of "control children".
         line->unparsestdout();

         // print out the variant tag, i.e. the type of statement.
         printf("STMT[%d] at line %d has variant:", 
                                      line->id(), line->lineNumber());
         printVariantName(line->variant());
         printf("\n");

         // is this a labeled statement? if so print the label.
         if(line->hasLabel()){
		SgLabel *lab = line->label();
                printf("has label[%d]\n", lab->id());
		}

         // are there comments that precede this statement?
         // if so print them out.
	 if(line->comments())
		printf("comments befor this line:\n%s", line->comments());
	
         // for each type of statement call the appropriate special case
         // function.	  
         switch(line->variant()){
               case GLOBAL:
                     printf("The head-of-fole global node. not really a statement\n");
                     break;
               case PROG_HEDR:
               case PROC_HEDR:
               case FUNC_HEDR:
                    printf(" a new routine.\n");
                    doRoutineHeader(line);
                    break;
               case BASIC_BLOCK	:
                    printf(" a beginning of a control block for C programs \n");
                    break;
               case CONTROL_END:
                    printf(" end of a control block for stmt %d\n",
                             (line->controlParent())->id());
                    break;
               case IF_NODE:
               case ELSEIF_NODE:
               case ARITHIF_NODE:
               case LOGIF_NODE:
                     doIfStmts(line);
                     break;
               case LOOP_NODE:
               case FOR_NODE:
               case FORALL_NODE:
               case WHILE_NODE:
                     doLoopStmts(line);
                     break;
               case EXIT_NODE:
                    // note the use of the special cast function
                    // we are casting to a subtype but this is o.k.
                    // with this function.
		    {SgExitStmt *   exst =  isSgExitStmt(line);
		     printf("an exit statement. exit from:\n");
		     doSymb(exst->constructName());
                     }
		     break;
               case ASSIGN_STAT:
		     { SgAssignStmt *ass =  isSgAssignStmt(line);
		     printf("an assignment\n");
                     // print out the two expressions on each side of =
		     printf("left hand side:\n");
			doExpr(ass->lhs());
		     printf("\nright hand side:\n");
			doExpr(ass->rhs());
                     printf("\n");
		     }
		     break;
               case PROC_STAT:
		    { int i;
                      SgCallStmt *call = isSgCallStmt(line);
                     // a "call f(...) statement.  extract the passed
                     // arguement expressions and print them.
                     printf("a subroutine call. passed args are\n");
		     for(i = 0; i < call->numberOfArgs(); i++){
			printf("argument %d:\n", i);
			doExpr(call->arg(i));
		        printf("\n");
			}
                      }
                     break;
               case WHERE_NODE:
               case ALLDO_NODE:
               case IDENTIFY:
               case FORMAT_STAT:
               case STOP_STAT:      break;
               case RETURN_STAT:    break;
               case GOTO_NODE:
               case ASSGOTO_NODE:
               case COMGOTO_NODE:
			doGoToStmt(line);
                        break;
               case VAR_DECL:
               case INTENT_STMT:        
               case OPTIONAL_STMT:
               case PUBLIC_STMT:
               case PRIVATE_STMT:
               case DIM_STAT:
               case ALLOCATABLE_STMT:
               case POINTER_STMT:
               case TARGET_STMT:
               case MODULE_PROC_STMT:
               case EXTERN_STAT:
               case COMM_STAT:
               case NAMELIST_STAT:
               case EQUI_STAT:
               case PARAM_DECL:
               case IMPL_DECL:
               case SAVE_DECL:
               case DATA_DECL:
			doVarDecl(line);
                        break;
               case PAUSE_NODE:     break;
               case STOP_NODE:      break;
               case ASSLAB_STAT:    break;
               case COMMENT_STAT:    break;
               case CONT_STAT:              
                    printf(" continue statement: end of cntl for stmt %d\n",
                             (line->controlParent())->id());
		    break;
               case ENTRY_STAT:
               case STMTFN_STAT:
               case BLOCK_DATA:
               case INTRIN_STAT:
               case PROC_COM:	/* process common */
               case ATTR_DECL:	/* attribute declaration */
                     printf("another fortran statement\n");
		     break;
                // the statements below are all valid, and will be
                // treated in example when I have more time.
               case READ_STAT:
               case WRITE_STAT:
               case PRINT_STAT:
               case BACKSPACE_STAT:
               case REWIND_STAT	:
               case ENDFILE_STAT:
               case INQUIRE_STAT:
               case OPEN_STAT:
               case CLOSE_STAT:
               case OTHERIO_STAT:
			doIOStmts(line);
                        break;
               case INCLUDE_STAT:
               case ALLOCATE_STMT:
               case NULLIFY_STMT:
               case DEALLOCATE_STMT:
               case SEQUENCE_STMT:
               case CYCLE_STMT:
               case EXIT_STMT:
               case CONTAINS_STMT:
               case WHERE_BLOCK_STMT:
               case MODULE_STMT:
               case USE_STMT:
               case INTERFACE_STMT:
               case OVERLOADED_ASSIGN_STAT:
               case POINTER_ASSIGN_STAT:
               case OVERLOADED_PROC_STAT:
                        printf("yet another fortran 90 statement.\n");
                        break;
               case DECOMPOSITION_STMT:  /* Old Fortran D stuff */
               case ALIGN_STMT:
               case DISTRIBUTE_STMT:
               case REDUCE_STMT:
                         printf("Old Fortran D. not treated here..needs update\n");
                         break;
               case CDOALL_NODE:  /* added for Cedar Fortran */
               case SDOALL_NODE:
               case DOACROSS_NODE:
               case CDOACROSS_NODE:
                        printf("Cedar Fortran.  who cares anymore. \n");
                        break;
               case PARDO_NODE:     /* Following added for PCF Fortran */
               case PARSECTIONS_NODE:
               case SECTION_NODE:
               case GUARDS_NODE:
               case LOCK_NODE:
               case UNLOCK_NODE:
               case CRITSECTION_NODE:
               case POST_NODE:
               case WAIT_NODE:
               case CLEAR_NODE:
               case POSTSEQ_NODE:
               case WAITSEQ_NODE:
               case SETSEQ_NODE:
               case ASSIGN_NODE:
               case RELEASE_NODE:
               case PRIVATE_NODE:
               case SCOMMON_NODE:
               case PARREGION_NODE:
               case PDO_NODE:
               case PSECTIONS_NODE:
               case SINGLEPROCESS_NODE:
               case SKIPPASTEOF_NODE:
                   printf("Old pcf fortran. needs update.  who cares anymore. \n");
		   break;
               default:
                   printf("unknown statement. not treated here..I am tired.\n");
                   break;
         }
   printf("---------------------------------------------------------------------\n");
    }
}
```