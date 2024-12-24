Проверяет корректность включенных в файл модулей.

Для этого использует функцию:
```cpp
/**
 * Cheching include ourselves
 * @param SgFile *file - poiter to checking file
 * @param string &fileName - name of the checking file
 * @param vector<Messages> &currMessages - vector of log messages, which can be appended
 * true - Cheching sucessfull
 * false - Cheching failed
 */
bool includeChecker(SgFile *file, const std::string &fileName, std::vector<Messages> &currM);
```

Проверки происходит 2:
- Проверка окончания блока комментария
- 


Зависимости:
- [[37 CORRECT_VAR_DECL]]


