Порядок выполнения [[passes]] проходов по программе.

1. [[93 LOOPS_SPLITTER]] и [[94 LOOPS_COMBINER]] включают режим fullDepGraph;

2. Если проход является корневым, то для него строится граф зависимостей

**Посмотреть зависимости можно в описании каждого прохода в [[passes]].**
**Добавить свои зависимости можно прописав их в InitPassesDependencies(...)**

3. Происходит инициализация DVM компилятора

4. Происходит создание проекта
Для этого вызывается дополнительный проход [[32 VERIFY_FUNC_DECL]]

5. Производится обход всех проходов из списка зависимостей

6. Производится целевой проход вместе с управляющими командами
**Для каждого прохода указаны уникальный условия запуска**

Отличаются следующие правила выполнения обходов:

[[41 FIND_FUNC_TO_INCLUDE]]
	Не запускает никаких анализов, но выполняет напрямую функцию ``static void findFunctionsToInclude(bool needToAddErrors)``
[[48 FILL_PAR_REGIONS_LINES]]
	Запускает анализ  ``runAnalysis(*project, curr_regime, false)``
	Проверяет, инициализированы ли флаги для всех параллельных регионов.
	Если нет, то инициализирует.
[[17 INSERT_PARALLEL_DIRS_NODIST]]
	Включает ``sharedMemoryParallelization``
	Использует папку по умолчанию ``__shared``
	Запускает сразу группу проходов и анализов:
- ``runAnalysis(*project, CREATE_PARALLEL_DIRS, false);``
- ``runPass(REVERT_SUBST_EXPR_RD, proj_name, folderName);``
- ``runPass(CONVERT_LOOP_TO_ASSIGN, proj_name, folderName);``
- ``runPass(REVERT_SUBST_EXPR_RD, proj_name, folderName);``
- ``runAnalysis(*project, INSERT_PARALLEL_DIRS, false, consoleMode ? additionalName.c_str() : NULL, folderName);``
- ``runPass(RESTORE_LOOP_FROM_ASSIGN, proj_name, folderName);``
- ``runAnalysis(*project, INSERT_REGIONS, false);``
- ``runAnalysis(*project, REMOVE_COPIES, false);``
- ``runAnalysis(*project, SWAP_LOOPS, false);``
И в случае если задан режим консоли или указано имя папки вызывается ещё 
``runAnalysis(*project, UNPARSE_FILE, true, additionalName.c_str(), folderName);``
[[16 INSERT_PARALLEL_DIRS]]
	Запускает для каждого параллельного варианта запускает проходы:
- ``runPass(CREATE_PARALLEL_DIRS, proj_name, folderName);``
- ``runPass(REVERT_SUBST_EXPR_RD, proj_name, folderName);``
- ``runPass(CONVERT_LOOP_TO_ASSIGN, proj_name, folderName);``
- ``runAnalysis(*project, INSERT_PARALLEL_DIRS, false, consoleMode ? additionalName.c_str() : NULL, folderName);``
	Если так же отключена ``sharedMemoryParallelization``, то будут выполнены ещё 
- ``runPass(CREATE_REMOTES, proj_name, folderName);``
- ``runPass(REMOVE_AND_CALC_SHADOW, proj_name, folderName);``
- ``runPass(SHADOW_GROUPING, proj_name, folderName);``
- ``runPass(TRANSFORM_SHADOW_IF_FULL, proj_name, folderName);``
- ``runAnalysis(*project, INSERT_SHADOW_DIRS, false, consoleMode ? additionalName.c_str() : NULL, folderName);``
	После чего запускает ``runPass(RESTORE_LOOP_FROM_ASSIGN, proj_name, folderName);``           

	Если так же отключена ``sharedMemoryParallelization``, то будут выполнены ещё 
	``runPass(ADD_TEMPL_TO_USE_ONLY, proj_name, folderName);``
	После чего запускает  ``runAnalysis(*project, INSERT_REGIONS, false);``
	Если так же отключена ``sharedMemoryParallelization``, то будут выполнены ещё 
	``runPass(GROUP_ACTUAL_AND_REMOTE, proj_name, folderName);``
	После чего запускает  
	``runAnalysis(*project, CALCULATE_STATS_SCHEME, false);``
	``runAnalysis(*project, REMOVE_COPIES, false);``
	``runAnalysis(*project, SWAP_LOOPS, false);``

[[4 CREATE_NESTED_LOOPS]]
[[1 CONVERT_TO_ENDDO]]
[[2 CORRECT_CODE_STYLE]]
[[54 INSERT_INCLUDES]]
[[55 REMOVE_DVM_DIRS]]
[[56 REMOVE_DVM_DIRS_TO_COMMENTS]]
[[90 PRIVATE_ARRAYS_EXPANSION]]
[[91 PRIVATE_ARRAYS_SHRINKING]]
[[0 UNROLL_LOOPS]]
[[84 INSERT_INTER_TREE]]
[[57 REMOVE_DVM_INTERVALS]]
[[107 SET_TO_ALL_DECL_INIT_ZERO]]
[[109 CREATE_CHECKPOINTS]]
[[113 PURE_INTENT_INSERT]]
[[130 REMOVE_OMP_DIRS_TRANSFORM]]
[[131 REMOVE_COMMENTS]]
[[134 INSERT_NO_DISTR_FLAGS_FROM_GUI]]
[[99 PRIVATE_REMOVING]]
[[136 RENAME_INLCUDES]]
	Просто вызывают анализ указанного типа:
	``runAnalysis(*project, curr_regime, true, "", folderName);`` 
[[86 INLINE_PROCEDURES]]
	Запускает анализ ``runAnalysis(*project, curr_regime, false);``
	И требует наличие ``folderName``, для запуска ``runAnalysis(*project, UNPARSE_FILE, true, "", folderName);``
[[6 UNPARSE_FILE]]
	Требует наличие ``folderName``, для запуска ``runAnalysis(*project, UNPARSE_FILE, true, "", folderName);``
[[39 CHECK_FUNC_TO_INCLUDE]]
	Просто запускает функцию обработки прямо отсюда
[[120 RENAME_SYMBOLS]]
[[51 RESOLVE_PAR_REGIONS]]
[[97 CREATE_PARALLEL_REGIONS]]
[[100 DUPLICATE_FUNCTIONS]]
[[112 CONVERT_STRUCTURES_TO_SIMPLE]]
[[114 PURE_COMMON_TO_PARAMS]]
[[115 PURE_SAVE_TO_PARAMS]]
[[116 PURE_MODULE_TO_PARAMS]]
[[117 REMOVE_UNUSED_FUNCTIONS]]
[[96 INSERT_REGIONS]]
[[93 LOOPS_SPLITTER]]
[[94 LOOPS_COMBINER]]
[[127 FIX_COMMON_BLOCKS]]
[[137 TEST_PASS]]
[[135 SET_IMPLICIT_NONE]]
	Просто вызывают анализ указанного типа:
	``runAnalysis(*project, curr_regime, false);`` 
[[65 SUBST_EXPR_RD_AND_UNPARSE]]
[[64 SUBST_EXPR_AND_UNPARSE]]
[[126 REMOVE_DEAD_CODE_AND_UNPARSE]]
	Требует наличие ``folderName``, для запуска 
	``runAnalysis(*project, curr_regime, true, "", folderName);`` 
[[88 ADD_TEMPL_TO_USE_ONLY]]
	Просто вызывают анализ указанного типа:
	``runAnalysis(*project, curr_regime, false, "", folderName);`` 
[[43 PRIVATE_ANALYSIS_SPF]]
	Проводит ``runAnalysis(*project, curr_regime, false);``, но только, если 
	``staticPrivateAnalysis`` включен.
[[105 PARSE_FILES]]
	Парсит файлы, согласно указанным там инструкциям.

Поведение по умолчанию:
	``runAnalysis(*project, curr_regime, false);``
	