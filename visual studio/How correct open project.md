Есть два способа открыть проект, что бы запускать его на исполнение. 

1.  Режим запуска исполнимого файла ==**без указания прохода**.== 
      Выбрать меню "Файл", далее "Открыть". 
      Выбрать "Папка", Visual Studio предложит показать папки, которые нужно открыть, укажите ==..sapfor\experts\Sapfor_2017==, где до sapfor путь к папке куда выполнен git clone. 
      Смотрите рисунок.![[Pasted image 20241203234229.png]]
2.     Режим запуска исполнимого файла ==**с указанием прохода**== (То что нам и нужно).
	   Выбрать меню "Файл", далее "Открыть". 
	   Выбрать "Решение или проект", Visual Studio предложит ткнуть ему пальцем, что нужно открыть. Наш выбор это ==..sapfor\experts\Sapfor_2017\build==, и конкретно файл **==ALL_BUILD.vcxproj==**. 
	   Далее необходимо открыть "Обозреватель решений". ![[Pasted image 20241204000618.png]]
	Нажать ПКМ на Sapfor_F и выбрать опцию "Выбрать в качестве запускаемого проекта".
	Нажать ПКМ на Sapfor_F, открыть "Свойства", перейти в раздел указанный на рисунке и задать аргументы исполнимого файла в окне редактирования "Аргументы команды".![[Pasted image 20241204000907.png]]
