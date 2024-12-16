Многие операторы содержат выражения. [[SgExpression]] является базовым классом для всех выражений. В отличие от иерархии классов [[SgStatement]], для каждого типа оператора выражения не существует подкласса. Базовые двоичные операторы, такие как стандартные арифметические операторы, идентифицируются только целочисленным вариантом, возвращаемым функцией-членом SgExpression variant(). Узлы выражений, имеющие свой собственный подкласс, делают это, потому что у них есть конструктор специального типа или специальные поля.

All Languages:
- [[SgExpression]]
- [[SgValueExp]]
- [[SgFunctionRefExp]]
- [[SgFunctionCallExp]]
- [[SgExprListExp]]
- [[SgVarRefExp]]
- [[SgArrayRefExp]]
- [[SgInitListExp]]
C:
- [[SgRecordRefExp]]
- [[SgPntrArrRefExp]]
- [[SgPointerDerefExp]]
- [[SgFuncPntrExp]]
- [[SgSubscriptExp]]
- [[SgUnaryExp]]
- [[SgCastExp]]
- [[SgExprIfExp]]
C++:
- [[SgDeleteExp]]
- [[SgNewExp]]
- [[SgThisExp]]
Fortran:
- [[SgKeywordValExp]]
- [[SgRefExp]]
- [[SgVecConstExp]]
- [[SgObjectListExp]]
- [[SgSpecPairExp]]
- [[SgIOAccessExp]]
- [[SgImplicitTypeExp]]
- [[SgTypeExp]]
- [[SgSeqExp]]
- [[SgStringLengthExp]]
- [[SgDefaultExp]]
- [[SgLabelRefExp]]
Fortran 90:
- [[SgConstExp]]
- [[SgStructConstExp]]
- [[SgAttributeExp]]
- [[SgKeywordArgExp]]
- [[SgUseOnlyExp]]
- [[SgUseRenameExp]]


