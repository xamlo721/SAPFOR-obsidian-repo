```cpp
#define TRUE  1
#define FALSE 0

extern "C"
int IsFortran() {
  SgFile *file;

  file = &(project->file(0));
  if (file->languageType() == ForSrc)
    return TRUE;
  else 
    return FALSE;
}
```