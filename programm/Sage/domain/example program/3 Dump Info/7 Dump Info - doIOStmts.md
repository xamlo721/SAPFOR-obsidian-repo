```cpp
// print out info about I/O statements.
// not done.
         
void doIOStmts(SgStatement *s){
SgIOStmt *   iost; 
SgInputOutputStmt * inoust;   
SgIOControlStmt *  iocntl;  
   if (iost = isSgIOStmt(s)){}
   else if(inoust = isSgInputOutputStmt (s)){}
   else if(iocntl = isSgIOControlStmt(s)){};
}

// print out the information about the different types of
// goto statements.  
// not done.  only does standard goto's.
```