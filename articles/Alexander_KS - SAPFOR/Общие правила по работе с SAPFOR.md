Перед началом работы с репозиторием необходимо убрать настройку git по автоматической замене LF -> CRLF

- либо командой git config --global core.autocrlf false
- либо командой git config --local core.autocrlf false

Инструкция по SAPFOR находится в Вики этого репозитория.

Проект Диалоговой оболочки (Визуализатора): [http://dvmh-server.ddns.net:3000/M/VisualSapfor](http://dvmh-server.ddns.net:3000/M/VisualSapfor)

Инструкция для установки и настройки Диалоговой оболочки: [https://cloud.mail.ru/public/NDxu/LJJhQgQUG](https://cloud.mail.ru/public/NDxu/LJJhQgQUG)

Правила оформления кода в проекте:

1. В проекте не должно быть табуляций - необходимо использовать пробелы.
2. Используется стандартный отступ в 4 пробела.
3. Каждая открывающая { и закрывающая } ставится на отдельной строке.
4. Если тело составного оператора состоит из одного оператора, то { } не ставятся.
5. Если тело составного оператора состоит из одного оператора, но данный оператор входит в другой составной оператор с количеством операторов более одного, то { } ставятся у всех составных операторов.
6. Все функции, которые используются только в файле объявления, должны иметь атрибут static.


Источник:
http://alex-freenas.ddns.net:3000/Alexander_KS/SAPFOR.git