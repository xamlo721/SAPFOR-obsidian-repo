1. В поле Компилятор указываем путь к нужному драйверу dvm_drv. Если соответствующий компилятор добавлен, он появится в выпадающем списке;

2. Указываем нужную команду линковки. В случае если главная программная единица на Fortran, указываем «flink», если на C — «clink».

**Другие команды линковки в DVM-системе использовать запрещено! **

3. Указываем флаги линковки, если они есть. 

**Запрещается указывать флаг «-o», или аналогичные ему, отвечающие за имя результирующего бинарного файла. Запрещается указывать флаги, отвечающие за стиль файлов (например «-free», «-f90» и т д). В этом случае система выдаст соответствующее сообщение.**

Только для DVM системы, существует возможность «назначить опции компилятора» через графический интерфейс, и задать их значения ( синие строчки кликабельны). По отметке галочками нужных опций, и задании их значений если они требуются, следует нажать «ОК», тогда в качестве флагов makefile появится заданные флаги через пробелы. При этом должны присутствовать текущие машина и пользователь— для запроса данных у компилятора.
![[Pasted image 20241124104526.png]]
![[Pasted image 20241124104535.png]]
После успешного добавления модуля линковки (в таблице отмечается как makefile), появляются языковые модули, и их нужно заполнить по мере необходимости.

![[Pasted image 20241124104555.png]]
![[Pasted image 20241124104607.png]]
Языковой модуль включается в финальный текст инструкции make, если в проекте присутствуют файлы соответствующего языка, и он активен, то есть отмечен галкой. Например, в случае если мы собираемся компилировать только часть проекта, написанную на Фортране, остальным модулям нужно снять галки одиночным нажатием мыши.
![[Pasted image 20241124104622.png]]
Заполнение языковых модулей для DVM-системы аналогично модулю линковки, за исключением команды компиляции. Для языков используются только следующие команды: 
- Fortran — «f»; 
- Cи — «с». 
Прочие языки программирования DVM-системой не поддерживаются. Если в проекте присутствуют части на С++, для них следует указать другой компилятор.

Правильно настроенный makefile для DVM-системы выглядит примерно так.
![[Pasted image 20241124104706.png]]
В случае других компиляторов принцип аналогичен, за исключением команды линковки/компиляции. Она должна быть пустой.

![[Pasted image 20241124104719.png]]


