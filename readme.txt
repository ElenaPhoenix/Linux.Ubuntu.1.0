sudo apt update - при каждом включении системы + создание снимков при каждом выключении
sudo apt upgrage - раз в неделю
sudo reboot - перезагрузка

clear - очистка терминала

https://losst.pro/prikolnye-komandy-linux
sudo apt install cowsay
	cowthink -f dragon "Сейчас все сожгу"
	cowsay -f eyes "Привет мир!"

sudo apt-get install sl
	sl
	sl -l - едущий поезд
	sl -laF

sudo apt-get install cmatrix
	cmatrix

sudo apt-get install xcowsay
	xcowsay "Привет!"

history - история всех команд
tree - дерево файлов
ll - просмотр всех файлов убунту
cd имя_папки - провалиться в эту папку
cd .. - подняться на уровень выше
cd -- - вернуться назад
cd <нажать кнопку TAB> - подгрузятся разные варианты файлов для постройки пути


ls - список файлов
	ls -a
	ls -alF - подробный список всех файлов текущего каталога

	ls --help - краткая справка о команде
	man ls - подробная документация о команде
pwd - показать текущую директорию (удобно получать абсолютный путь)
mkdir - создание каталога
cp - копирование
rm - удаление
	rm -r название_директории - удаление директории
mv - переименование/перенос
touch - создание пустого файла/изменение его свойств
cat - вывод файла, склейка, создание
	cat имя_файла - распечатывает содержимое файла в терминал
	cat > название_файла - перезапись всего файла (ниже написать текст)
	cat >> название_файла - дополнение файла новым текстом
	ll | cut -f 1 -d " " - вывод первой колонки списка до разделителя "пробел"
echo "какой-то_текст" >/>> название_файла - перезапись/дополнение файла

ls -ali - список всех жестких ссылок (дубликатов)

Текстовые редакторы
vim
	wq запись и выход
nano
Mcedit

Пейджеры 
less
more


			Права доступа и безопасность
Категории пользователей:
u - владелец файла;
g - группа файла;
o - все остальные пользователи;

три основных вида прав:
r - чтение;
w - запись;
x - выполнение;
s - выполнение  от имени суперпользователя (дополнительный);

0 --- ;
1 --x; 
2 -w-; 
3 --wx; 
4 r--; 
5 r-x; 
6 rw-; 
7 rwx

chmod 777 название файла - присвоить все права всем
chmod +x

tail /etc/passwd – список пользователей
tail /etc/group – группы пользователей
tail /etc/shadow – пароли пользователей

sudo adduser
sudo useradd
sudo groupadd  название_группы - добавить группу

su имя_пользователя - зайти от имени этого пользователя
sudo usermod -aG название_группы имя_пользователя - добавить доп.группу пользователю
chown

ugo - r - всем запрет читать
ugo - rwx - запрет на все всем

groups имя_пользователя - список всех групп пользователя
id
less /etc/group - все группы существующие в системе
less /etc/passwd - все пользователи
sudo userdel имя_пользователя - удалить пользователя
	sudo userdel -f имя_пользователя - принудительно удалить пользователя
	sudo groupdel

			Скрипты Bash
#!/bin/bash - прочитать с помощью баш, в самом начале файла
echo $? - код завершения
ps afx - вывод списка процессов
printenv - все переменные окружения системы

переменные начинаются с $
первоначально всё определяется башем как строка.

type название_команды - тип команды
	type -a название_команды - подробнее о типе команды

nano .bashrc - можно изменить под себя, создать короткие команды и носить с собой между окружениями


			Настройка сети. https://www.youtube.com/watch?v=2NjjmwMT4nY
ip
ip address show
sudo ip address add 192.168.1.254 (придумать рандомный адрес) dev enp0s3 - добавить новый айпи адрес
sudo ip address del 192.168.1.254/32 (придуманный рандомный адрес) dev enp0s3 - удалить айпи адрес

ping yandex.ru адрес_вебстраницы - проверка возможности подключиться к странице
host google.com

sudo apt install net-tools - установка утилиты для работы с сетями
route - Таблица маршрутизации ядра протокола IP
sudo route add -host 192.168.1.254 (придумать рандомный адрес) reject
sudo iptables -L - можно запрограммировать разные айпи адреса под разные возможности
sudo iptables -A INPUT -s 20.20.20.20 -j DROP - добавляем новый айпи адрес в сеть с запретом подключения
sudo iptables -A FORWARD -s 2.2.2.2 -j ACCEPT -
sudo iptables -A INPUT -s 20.20.20.20/24 -j DROP - добавляем новый айпи адрес(с маской последние 20.20 динамические айпи адреса до 24) в сеть с запретом подключения
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT - любой может подключиться по протоколу tcp к порту 22 и получить доступ к хосту 

ps
ps afx - таблица процессов
kill -9 2410 - уничтожить файл, -9 - полный приоритет


			Веб-сервера
sudo apt install nginx
ss -ntlp
sudo systemctl start nginx
sudo nginx -t - тест
curl localhost:8080
sudo systemctl reload nginx - перезагрузка nginx после внесенных изменений

sudo apt install apache2
sudo apachectl -t - тест
systemctl start apache2
systemctl status apache2 - просмотр статуса соединения
sudo systemctl reload apache2
Корректность конфигурации веб сервера Apache можно проверять командой 'apachectl -t'.
sudo systemctl stop nginx
sudo systemctl stop apache2

apt install php8.1 libapache2-mod-php8.1
apt install php8.1-fpm
apt install mysql-server-8.0

sudo mysql - консоль mysql
	show databases;
	use mysql; - войти
	mysql -u root -p;
	show tables;
	SELECT * FROM user\G;
	CREATE DATABASE название_базы_данных;
	CREATE TABLE название_таблицы (i INT);
	INSERT INTO название_таблицы (i) VALUES (1),(2),(3),(4);
	SELECT * FROM название_таблицы - вывод всей таблицы
	CREATE USER 'имя_пользователя'@'ip_адрес(напр, localhost)' IDENTIFIED BY 'задать_пароль';
		mysql -u логин -p - войти в mysql от пользователя
	exit - выход из mysql

sudo apt -y install php-mbstring
sudo apt -y install phpmyadmin 				12345678
CREATE USER 'test'@'localhost' IDENTIFIED BY 'пароль';
GRANT ALL PRIVILEGES ON *.* TO 'test'@'localhost';
FLUSH PRIVILEGES;
https://losst.pro/ustanovka-phpmyadmin-ubuntu-18-04

			Основы Docker
sudo apt install docker.io
sudo docker - справка по режимам использования
docker run название_образа - создает и запускает контейнер
docker ps - список запущенных контейнеров
docker ps -a - список всех контейнеров
docker search nginx - поиск образа
docker images - список образов
docker rm имя_образа(/id_контейнера) - удаление контейнера
docker rmi имя_образа - удаление образа
docker pull имя_образа - скачивание образа без запуска
docker history имя_образа - история какие этапы проходил контейнер при сборке
docker run -d --restart always -p 80:80 -v /var/www/html:/usr/share/nginx/html --name nginx1 nginx - запускать всегда при запуске системы по портам 80:80 откуда брать инфу для загрузки придумать_имя_контейнера имя_образа
iptables -L -nv

docker exec -ti nginx1 bash - зайти внутрь контейнера через оболочку bash
	exit
docker logs nginx1 - просмотреть логи

apt install docker-compose
apt install yamllint - проверка yml
docker-compose up -d -  создание и запуск
digitalocean.com/community/tutorials/how-to-install-wordpress-with-docker-compose#step-1-defining-the-web-server-configuration

Рекомендуемая литература (для более глубокого изучения Linux):
• Unix и Linux: руководство системного администратора - Немет Эви
• Современные операционные системы - Эндрю Таненбаум
• Ядро Linux - Бовет Даниэль
Linux API. Исчерпывающее руководство - Майкл Керриск


docker run hello-world

https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-docker-compose#step-1-defining-the-web-server-configuration
wordpress - конструктор сайтов



sudo docker search ubuntu
sudo docker run ubuntu
docker run -d ubuntu

Сборка образа из Dockerfile производится командой "docker build". 
Утилита docker-compose также позволяет выполнять основные манипуляции с контейнерами. 
Справка: docker-compose --help
Правильно, что используете ключ -d в команде docker run, чтобы освободить консоль для ввода других команд.







