
# Получение SAPFOR (OC Linux)

По [ссылке](<https://cloud.mail.ru/public/3rMc%2FaRqYCZ33N>) и скачать архив
![[Visualizer_linux.zip]]

Распаковать в отдельную папку, в пути до которой не должно быть русских букв.

По [ссылке](<https://cloud.mail.ru/public/3rMc/aRqYCZ33N/Linux_Visualizer>) скачать «checkUniq.cpp» и «server.cpp»

![[server.cpp]]
![[checkUniq.cpp]]

и положить в папку с предыдущим архивом в корень.


## Требования:

### JRE
Для запуска требуется ОФИЦИАЛЬНАЯ JRE 1.8
проверить можно через 
```
java -version
```

![[Pasted image 20241117182035.png]]
желательно обновить до последней версии.

Как установить jdk8 на linux должны знать уже дети.

Может потребоваться установка её в качестве основной, через:

```
sudo update-alternatives --config java
```

## Сборка
Собрать проект через 
```
g++ -O3 -std=c++17 checkUniq.cpp server.cpp -o Visualizer_2 -lpthread -lstdc++fs
```
Должна получиться такая структура:
![[Pasted image 20241117211029.png]]

