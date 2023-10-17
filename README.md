# Контейнеризация (семинары)

![picture for containerization](img/bd786e1b-aac5-4164-a56e-ccae5c3d6864.jpeg)

## Урок 5. Docker Compose и Docker Swarm

### **Информация о проекте**

Создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД (compose)

- Запускаем и скачиваем два контейнера:

``` bash

docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:8.0.31

docker run --name myphp -d --link some-mysql:db -p 8081:80 phpmyadmin/phpmyadmin

```
![picture1](img/Screenshot%20from%202023-10-17%2012-26-29.png)

- Проверяем работоспасобность, заходим в браузере на localhost:8081

![picture2](img/Screenshot%20from%202023-10-17%2012-30-25.png)

- Чтобы запустить compose, создадим папку и файл docker-compose.yml:

``` bash

sudo mkdir /folderforcompose

cd /folderforcompose/

sudo nano docker-compose.yml

#Прописываем в yml файле:
version: '3.1'


services:

	db:

		image: mariadb:10.10.2

		restart: always

		environment:

			MYSQL_ROOT_PASSWORD: 12345



	adminer:

		image: adminer:4.8.1

		restart: always

		ports:

			- 6080:8080

```

![picture3](img/Screenshot%20from%202023-10-17%2013-00-31.png)

``` bash
docker-compose up -d
```

![picture4](img/Screenshot%20from%202023-10-17%2013-04-04.png)

Проверяем:

![picture5](img/Screenshot%20from%202023-10-17%2013-04-58.png)

*Подготовила студентка Geek Brains* [**`Эрина Ксения`**](https://github.com/MoraKsu)