```cpp  
/*********************************************************************/
/*                  pC++/Sage++  Copyright (C) 1993                  */
/*  Indiana University  University of Oregon  University of Rennes   */
/*********************************************************************/

#include <stdio.h>
#include <malloc.h>
#define DISTRIBUTION
#include "sage++user.h"

#define MAXSUBS 100

struct ftable {
  char *function_name;
  SgStatement *function;
} ftable;

struct ftable function_table[MAXSUBS];
int totalfunctions;
static int event = 0;
SgProject *project;
```

[[1 Instrument - Fortran Program Transformations]]
[[2 Instrument - InitSymbols]]
[[3 Instrument - InitFunctionTable]]
[[4 Instrument - InsertFCallNode]]
[[5 Instrument - FixLoops]]
[[6 Instrument - FInstrumentSub]]
[[7 Instrument - FInitialize]]
[[8 Instrument - FInstrument]]
[[9 Instrument - ProjectUnparse]]
[[10 Instrument - UnparseSub]]
[[11 Instrument - VistaInstrument]]
[[12 Instrument - FAnalyze]]
[[13 Instrument - pC++ Program Transformations]]
[[14 Instrument - isReferenceToMethodOfElement]]
[[15 Instrument - isReferenceToClassOfElement]]
[[16 Instrument - inMethodOfTheElement]]
[[17 Instrument - whichFunctionAmI]]
[[18 Instrument - isReferenceToCollection]]
[[19 Instrument - ListCollections]]
[[20 Instrument - ListCollectionInstances]]
[[21 Instrument - ListCollectionInvocations]]
[[22 Instrument - CAnalyze]]
[[23 Instrument - CInitSymbols]]
[[24 Instrument - CInitialize]]
[[25 Instrument - InsertCCallNode]]
[[26 Instrument - CTimingInstrumentSub]]
[[27 Instrument - CTimingInstrument]]
[[28 Instrument - OpenProject]]
[[29 Instrument - IsFortran]]
[[30 Instrument - IsC]]









