# Задание
Создать 2 докер-приложения {username}/user1, {username}/user2
 * создать Dockerfile-ы на базе https://hub.docker.com/_/nginx/
 * приложения должны отличаться от базового только файлом index.html, для первого там должна быть фраза "Hello user1!", для второго "Hello User2!"
 * созданные докер образы должны быть запушены на docker hub
 *  исходный код (Dockerfile-ы ...) для каждого приложения должен быть залит в отдельные репозитории на github {username}/user1, {username}/user2



Проверка:
docker run -d -p 81:80 {username}/user1
docker run -d -p 82:80 {username}/user2

curl http://localhost:81/index.html - результат должен содержать "Hello User1!"
curl http://localhost:82/index.html - результат должен содержать "Hello User2!"


#Выполнение
#################################################################################

# 1 - Создаем файл Dockerfile

nano Dockerfile

FROM debian

RUN apt-get -y update
RUN apt-get -y install nginx

RUN echo 'Hello user2!' > /var/www/html/index.html


CMD ["/usr/sbin/nginx", "-g", "daemon off;"]

# 2- Создание нового образа
docker build -t user:v2 .
# 3 - Запуск
docker run -d -p 82:80 user:v2

# 4 - Проверка
curl http://localhost:82/index.html

