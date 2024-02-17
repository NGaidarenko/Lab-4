# Лабораторная работа №4
## Задача
#### Запустить в контейнере приложение `cowsay`. Далее в рамках лабораторной работы необходимо самостоятельно настроить сеть между двумя контейнерами и протестировать соединение между контейнерами утилитой ping.
#### 

## Решение задачи
#### Создадим файл и изменим его используя команды:
```
touch Dockerfile
gedit Dockerfile
```
После напишем в нашем файле:
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/gedit_file.jpg)
Строка `RUN apt-get install -y iputils-ping` устанавливает утилиту ping, которая нам понадобиться для проверки сети между контейнирами.
#### 
#### Далее в двух терминалах запускаем программу сборки используюя команду `docker build -t cowsay .` Получим:
![Первый терминал](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/build_1.jpg)
![Второй терминал](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/build_2.jpg)
#### 
#### Далее можем запустить контейнер и подключиться к нему напрямую командой `docker run -it cowsay`, это обеспечит работу контейнера в фоновом режиме.
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/run_1.jpg)
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/run_2.jpg)
#### 
#### Открываем еще одно окно терминала и создаем сеть при помощи команды `docker network create newNetwork`
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/networkCreate.jpg)
#### 
#### После этого подключим наши контейнеры к нашей сети, используя конманды
```
docker network connect myNetwork mycontainer1
docker network connect myNetwork mycontainer2
```
Но необходимо узнать названия контейнеров, для этого используем команду `docker ps` и получим:
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/docker_ps.jpg)
#### 
Получается первый контейнер называется `quirky_torvalds`, а второй контейнер называется `epic_wiles`.
#### Используем комнды, которые мы указывали ранее для подключения наших контейнеров к нашей сети, получим:
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/connect_network.jpg)
#### 
#### Проверим настройки созданной сети при помощи команды `docker network inspect myNetwork`:
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/inspect_network.jpg)
#### Далее необходимо протестировать соединение между контейнерами утилитой ping, используя команды `docker exec -it <название контейнера 1/2> ping <ip контейнера 2/1>`
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/ping_1.jpg)
![](https://github.com/NGaidarenko/Lab-4/blob/main/images_lab_5/ping_2.jpg)
#### 
## Вывод
#### Получилось запустить в двух контейнерах приложение `cowsay`. Также была настроена сеть между контейнерами и проверенно соединение при помощи утилиты `ping`.


