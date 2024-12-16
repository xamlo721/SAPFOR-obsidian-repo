Методы атрибутов, предназначенные для использования с объектами SgStatement, SgExpression, SgType и SgSymbol. 

Атрибуты могут быть присоединены к объектам SgStatement, SgExpression, SgType или SgSymbol. Доступны следующие методы:

`int **numberOfAttributes**`**()**

Указывает количество атрибутов, присоединенных к объекту SgStatement (или SgExpression, SgSymbol, SgType).

`int **numberOfAttributes**`**(int type)**

Указывает количество атрибутов типа type, прикрепленных к объекту. Параметр type действует как фильтр.

`void ***attributeValue**`**(int i)**

Возвращает поле данных i-го атрибута (i=0,1,..), привязанного к узлу. Возвращает значение NULL, если узел не существует.

`int **attributeType**`**(int i)**

Возвращает тип i-го атрибута (i=0,1,..), привязанного к узлу. Возвращает 0, если узел не существует.

`void ***attributeValue**`**(int i,int type)**

То же, что и AttributeValue(int i), но учитывает только атрибут type type.

`void ***deleteAttribute**`**(int i)**

Удаляет i-й атрибут (i=0,1,..) в списке атрибутов объекта. Поле данных возвращается, поэтому при необходимости его можно удалить.

`void **addAttribute**`**(int type, void *a, int size)**

Добавляет атрибут к узлу. Ограничений нет (кроме объема доступной памяти).

`void **addAttribute**`**(int type)**

Добавляет атрибут без поля данных. Поле данных имеет значение NULL.

`void **addAttribute**`**(void *a, int size)**

Добавляет атрибут, содержащий только поле данных.

`void **addAttribute**`**(SgAttribute *at)**

Добавляет атрибут, который уже был создан.

`SgAttribute ***getAttribute**`**(int i)**

Возвращает i-й (i=0,1,..) атрибут объекта.

`SgAttribute ***getAttribute**`**(int i,int type)**

Возвращает i-й атрибут типа type, прикрепленный к объекту.