Представляет указатели на языке Си, используемые в качестве массивов.
```cpp
class **SgPntrArrRefExp**: public SgExpression {
public:
  inline SgPntrArrRefExp(PTR_LLND ll);
  inline SgPntrArrRefExp(SgExpression &p;);
  inline SgPntrArrRefExp(SgExpression &p;, SgExpression &subscripts;);
  inline SgPntrArrRefExp(SgExpression &p;, int n, SgExpression &sub1;, 
                         SgExpression &sub2;);
  inline SgPntrArrRefExp(SgExpression &p;, int n, SgExpression &sub1;, 
                         SgExpression &sub2;, SgExpression &sub3;);
  inline SgPntrArrRefExp(SgExpression &p;, int n, SgExpression &sub1;, 
                         SgExpression &sub2;, SgExpression &sub3;, 
                         SgExpression &sub4;);
  inline ~SgPntrArrRefExp();
  inline int dimension();  // the number of subscripts in reference
  inline SgExpression *subscript(int i);
  inline void addSubscript(SgExpression &e;);
  inline void setPointer(SgExpression &p;);
};
```

#### Члены класса 
`**SgPntrArrRefExp**`**(PTR_LLND ll)**

document me

`**SgPntrArrRefExp**`**(SgExpression &p;)**

document me

`**SgPntrArrRefExp**`**(SgExpression &p;, SgExpression &subscripts;)**

document me

`**SgPntrArrRefExp**`**(SgExpression &p;, int n, SgExpression &sub1;, SgExpression &sub2;)**

document me

`**SgPntrArrRefExp**`**(SgExpression &p;, int n, SgExpression &sub1;, SgExpression &sub2;, SgExpression &sub3;)**

document me

`**SgPntrArrRefExp**`**(SgExpression &p;, int n, SgExpression &sub1;, SgExpression &sub2;, SgExpression &sub3;, SgExpression &sub4;)**

document me

`int **dimension**`**()**

document me

`SgExpression ***subscript**`**(int i)**

document me

`void **addSubscript**`**(SgExpression &e;)**

document me

`void **setPointer**`**(SgExpression &p;)**

document me





