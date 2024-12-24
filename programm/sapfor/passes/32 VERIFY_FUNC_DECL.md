	 Проверка корректность объявления. А конкретно: проверка двойного объявления функций и проверка зарезервированного имени функции.

Является базовым проходом для большинства проходов.

Сигнатура:

```cpp
/**
 * The function checks the correctness of the declaration. 
 * Specifically: checking for double declaration of functions and checking for a reserved function name.
 * @return 0 if checks failed 
 * @return 1 if checks sucessfully
 */
bool verifyFunctionDeclaration(SgFile *file, map<string, pair<string, int>> &funcNames, map<string, vector<Messages>> &currMessages) {

```

Зависимости:
	Нет зависимостей.

