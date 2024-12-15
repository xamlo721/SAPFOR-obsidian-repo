```cpp
// Fortran program transformations

SgType *SgTypeInt();

SgSymbol *entry, *eexit, *loop_entry, *loop_exit;
char *fnames[] = {"entry_event", 
		  "exit_event", 
		  "loop_entry_event", 
		  "loop_exit_event"};

#define ENTRY_EVENT 0
#define EXIT_EVENT  1
#define LOOP_ENTRY  2
#define LOOP_EXIT   3

#define AFTER  0
#define BEFORE 1
```