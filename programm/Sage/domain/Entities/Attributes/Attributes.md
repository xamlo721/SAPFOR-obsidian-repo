Можно добавлять информацию к узлам Sage, используя атрибуты. Атрибут имеет два значения:

1 type: типы, предоставленные пользователем, должны быть целыми положительными числами; целые отрицательные числа зарезервированы для системы; зарезервированными типами являются:
```cpp
	#define DEPENDENCE_ATTRIBUTE -1001 
     #define INDUCTION_ATTRIBUTE -1002 
     #define ACCESS_ATTRIBUTE -1003 
     #define DEPGRAPH_ATTRIBUTE -1004 
     #define USEDLIST_ATTRIBUTE -1005 
     #define DEFINEDLIST_ATTRIBUTE -1006 
     #define NOGARBAGE_ATTRIBUTE -1007 
     #define GARBAGE_ATTRIBUTE -1008 
     #define ANNOTATION_EXPR_ATTRIBUTE -1009
```
 2 data: поле данных - это указатель на void, который можно использовать для хранения любой информации.
 
Пожалуйста, смотрите раздел Вычисления зависимости данных для Fortran для получения примеров использования атрибутов.

