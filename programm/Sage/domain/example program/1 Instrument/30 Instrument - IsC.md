```cpp
extern "C"
int IsC() {
  SgFile *file;

  file = &(project->file(0));
  if (file->languageType() == CSrc)
    return TRUE;
  else 
    return FALSE;
}
```