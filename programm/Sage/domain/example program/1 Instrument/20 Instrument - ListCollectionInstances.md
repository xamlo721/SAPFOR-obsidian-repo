```cpp
void  ListCollectionInstances(SgFile *file) {
  SgType *type;
  SgDerivedCollectionType *c;

  for (type = file->firstType(); type ; type = type->next()){
    if (c = isSgDerivedCollectionType(type)){
      SgStatement *s;

      printf("%s<%s>\n",c->collectionName()->identifier(),
	               c->elementClass()->symbol()->identifier());
    }
  }
}
```