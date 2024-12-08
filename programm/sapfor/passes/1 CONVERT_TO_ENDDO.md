

Зависимости:
- [[37 CORRECT_VAR_DECL]]
- [[63 REVERT_SUBST_EXPR_RD]]
- [[29 VERIFY_INCLUDES]]


Вызывает анализ с следующими атрибутами:
``runAnalysis(*project, curr_regime, true, "", folderName);``

При этом имеет 2 стадии анализа

# FIRST STEP

Вызывает конвертацию ``ConverToEndDo(file, getObjectForFileFromMap(file_name, SPF_messages));``

# SECOND STEP
Проверяет флаг ``verifyOK``
Флаг находится в [[runAnalysis]] и проверяет корректно ли отработала фаза анализа проходов:
[[28 VERIFY_ENDDO]]
[[29 VERIFY_INCLUDES]]
[[58 VERIFY_DVM_DIRS]]
[[30 VERIFY_EQUIVALENCE]]
[[33 VERIFY_OPERATORS]]
[[34 VERIFY_FORMAT]]
[[31 VERIFY_COMMON]]
[[32 VERIFY_FUNC_DECL]]

Флаг не обязательно вообще устанавливался, т.к. остальные проходы могли и не вызываться. Если он не был поднят, то бросает исключение ``-1``. 