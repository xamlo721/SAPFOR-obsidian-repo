Устанавливает 
```cpp
sharedMemoryParallelization = 1;
ignoreArrayDistributeState = true;
keepDvmDirectives = 0;
ignoreIO = 1;
```
(ignore io checker for arrays (DVM IO limitations))

не может быть запущен для прохода ``INSERT_PARALLEL_DIRS``

```
[SAPFOR]: deprecated regime: pass == INSERT_PARALLEL_DIRS and -mpi option. Instead, you need to use INSERT_PARALLEL_DIRS_NODIST pass
```
