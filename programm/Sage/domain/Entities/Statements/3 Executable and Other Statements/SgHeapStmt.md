Представляет собой Fortran allocate и deallocate.

```cpp
class  **SgHeapStmt**: public SgExecutableStatement {
  // Fortran heap space allocation and deallocation statements
  // variant == ALLOCATE_STMT or DEALLOCATE_STMT 
public:
  inline SgHeapStmt(int variant, SgExpression &allocationList;, 
                    SgExpression &statVariable;);
  inline ~SgHeapStmt();
  inline SgExpression *allocationList();
  inline void setAllocationList(SgExpression &allocationList;);
  inline SgExpression *statVariable();
  inline void setStatVariable(SgExpression &statVar;);
};
```

#### Члены класса
`**SgHeapStmt**`**(int variant, SgExpression &allocationList;, SgExpression &statVariable;)**

document me

`SgExpression ***allocationList**`**()**

document me

`void **setAllocationList**`**(SgExpression &allocationList;)**

document me

`SgExpression ***statVariable**`**()**

document me

`void **setStatVariable**`**(SgExpression &statVar;)**

document me



