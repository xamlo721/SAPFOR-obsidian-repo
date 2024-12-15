```cpp
// help functions for classifyExpression
    
void doExpr(SgExpression *e){
    printf("EXPR[%d]:",e->id());
    e->unparsestdout();
}

int lhsId(SgExpression *e){
    if(e->lhs()) return (e->lhs())->id();
    else return -1;
}
int rhsId(SgExpression *e){
    if(e->rhs()) return (e->rhs())->id();
    else return -1;
}
int symbId(SgExpression *e){
    if(e->symbol()) return (e->symbol())->id();
    else return -1;
}
char * symbName(SgExpression *e){
    if(e->symbol()) return (e->symbol())->identifier();
    else return "";
}
int typeId(SgExpression *e){
    if(e->type()) return (e->type())->id();
    else return -1;
}

void classifyExpressions(SgFile *f){
    SgExpression *e;
    for(e = f->firstExpression(); e; e = e->nextInExprTable()){
       SgValueExp *valexp = isSgValueExp(e);
       printf("EXPR[%3d] ", e->id());
       switch(e->variant()){    
               case INT_VAL:
                    printf("integer value:%d ", valexp->intValue());
		    break;
               case FLOAT_VAL:
                    printf("real value:%f ", valexp->floatValue());
		    break;
               case DOUBLE_VAL:
                    printf("double value:%f ", valexp->doubleValue());
		    break;
               case BOOL_VAL:
                    printf("bool value:%i ", valexp->intValue());
		    break;
               case CHAR_VAL:
                    printf("char value:%c ", valexp->charValue());
		    break;
               case STRING_VAL:
                    printf("string value:%s ", valexp->stringValue());
		    break;
               case COMPLEX_VAL:
                     printf("complex: real part id=%d im part id=%d ",
                                       lhsId(e),rhsId(e));
		    break;
              case KEYWORD_VAL:   /* Strings to be printed with quotes */
			break;
               case CONST_REF:
		     printf("constant ref: symb[%d]:%s type[%d] ", 
                                 symbId(e), symbName(e), typeId(e));
                     break;
               case VAR_REF:
		     printf("variable ref: symb[%d]:%s type[%d] ", 
			          symbId(e), symbName(e), typeId(e));
		     break;
               case ARRAY_REF:
		     printf("array ref: symb[%d]:%s type[%d] subscript list id (%d) ", 
			          symbId(e), symbName(e), typeId(e), lhsId(e));
		     break;
               case RECORD_REF:   
               case LABEL_REF:
			break;
               case VAR_LIST:
               case EXPR_LIST:
               case RANGE_LIST:
                       printf("this item [%d]  next list [%d] ", lhsId(e), rhsId(e));
			break;
               case CASE_CHOICE:
               case DEF_CHOICE:
               case VARIANT_CHOICE:
			break;
               case DDOT:
               case RANGE_OP:
               case UPPER_OP:
               case LOWER_OP:
               case EQ_OP:
               case LT_OP:
               case GT_OP:
               case NOTEQL_OP:
               case LTEQL_OP:
               case GTEQL_OP:
               case ADD_OP:
               case SUBT_OP:
               case OR_OP:
               case MULT_OP:
               case DIV_OP:
               case MOD_OP:
               case AND_OP:
               case EXP_OP:
               case ARRAY_MULT:
               case CONCAT_OP:	/* cancatenation of strings */
               case XOR_OP:	/* .XOR. in fortran */
               case EQV_OP:	/* .EQV. in fortran */
               case NEQV_OP:	/* .NEQV. in fortran */
                       printf("left oprnd[%d] right oprnd[%d] ", lhsId(e), rhsId(e));
                      break;
               case MINUS_OP:	/* unary operations */
               case NOT_OP:
                       printf("operand   [%d]                 ", lhsId(e));
		      break;
               case STAR_RANGE:	/* operations with no operands 360.. */
		      break;
               case PROC_CALL:
               case FUNC_CALL:
               case CONSTRUCTOR_REF:
               case ACCESS_REF:
               case CONS:
               case ACCESS:
               case IOACCESS:
               case CONTROL_LIST:
               case SEQ:
               case SPEC_PAIR:
               case COMM_LIST:
               case STMT_STR:
               case EQUI_LIST:
               case IMPL_TYPE:
               case STMTFN_DECL:
               case BIT_COMPLEMENT_OP:
               case EXPR_IF:
               case EXPR_IF_BODY:
               case FUNCTION_REF:
               case UNARY_ADD_OP:
               case SIZE_OP:
               case INTEGER_DIV_OP:
               case SUB_OP:
               case NAMELIST_LIST:
               case ORDERED_OP:     /* Following added for PCF FORTRAN */
               case EXTEND_OP:
               case MAXPARALLEL_OP:
               case SAMETYPE_OP:
               case TYPE_REF:     /* Added for FORTRAN 90 */
               case STRUCTURE_CONSTRUCTOR:
               case ARRAY_CONSTRUCTOR:
               case SECTION_REF:
               case VECTOR_SUBSCRIPT:
               case SECTION_OPERANDS:
               case KEYWORD_ARG:
               case OVERLOADED_CALL:
               case INTERFACE_REF:
               case RENAME_NODE:
               case TYPE_NODE:
               case PAREN_OP:
               case PARAMETER_OP:
               case PUBLIC_OP:
               case PRIVATE_OP:
               case ALLOCATABLE_OP:
               case DIMENSION_OP:
               case EXTERNAL_OP:
               case IN_OP:
               case OUT_OP:
               case INOUT_OP:
               case INTRINSIC_OP:
               case POINTER_OP:
               case OPTIONAL_OP:
               case SAVE_OP:
               case TARGET_OP:
               case ONLY_NODE:
               case LEN_OP:
               case TYPE_OP:
               default:
                   break;
        }
    printf(" variant: ");
    printVariantName(e->variant());
    printf(" expr is: "); 
    e->unparsestdout();
    printf("\n");
    }
}
```