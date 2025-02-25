# Работа с пользователями

### Задание 1. Создание учетных записей
1.	Создайте учетную запись user1, путем прямого редактирования файла учетных записей.
```bash
sudo nano /etc/passwd
user1:x:1001:1001::/home/user1:/bin/bash
```
Для проверки, что учетная запись создана, выполнить:
```bash
id user1
```
2.	Создайте учетную запись user2, используя команду adduser.
Если команда выполнена без параметра -m, то домашняя директория не будет создана. 
```bash
sudo adduser -m user2
```
3.	Создайте учетную запись user3, используя команду pw.
Только для FreeBSD:
```bash
sudo pw useradd user3 -m
```
4.	Создайте учетную запись с правами администратора.
```bash
sudo adduser admin
sudo usermod -aG sudo admin
```
### Задание 2. Модификация учетных записей
1.	Задайте для пользователей user1 и user2 был общий домашний каталог /home/managers/.
```bash
sudo usermod -d /home/managers user1
sudo usermod -d /home/managers user2
```
2.	Заблокируйте учетную запись user3.
```bash
sudo usermod -L user2
```
Чтобы проверить блокировку учетной записи:
```bash
sudo nano /etc/shadow
```
Если учетная запись заблокирована строка содержит ! или * перед хешем пароля. 
3.	Заставьте пользователя user1 сменить пароль при следующем входе в систему.
```bash
sudo chage -d 0 user1
```
4.	Назначьте пользователю user1 в качестве командного интерпретатора по умолчанию csh.
```bash
sudo apt update
sudo apt install csh
sudo chsh -s /bin/csh user1
```
5.	Измените пароль администратора на 12345
```bash
sudo passwd admin
echo "admin:eltexoroot" | sudo chpasswd
```

### Задание 3. Создание групп и модификация групп
1.	Создайте группу managers
```bash
sudo groupadd managers
```
2.	Включите в группу managers пользователей user1, user2
```bash
sudo usermod -aG managers user1
sudo usermod -aG managers user2
```

Задание 4. Выполнение команд от имени других пользователей
1. Изучите дополнительные команды для работы с учетными записями: whoami, id, last, users
```bash
whoami — показывает имя текущего пользователя.
id — показывает UID и GID текущего пользователя.
last — показывает список последних входов в систему.
users — показывает список текущих пользователей, вошедших в систему.
```
2.	Разрешите пользователю user1 выполнять команды от имени суперпользователя, использую команду su.
```bash
sudo usermod -aG sudo user1
sudo visudo
user1 ALL=(ALL:ALL) ALL
```
3.	Разрешите пользователю user2 выполнять любые команды, кроме перезагрузки и завершения работы ОС.
команду su.
```bash
sudo visudo
user2 ALL=(ALL) ALL, !/sbin/shutdown, !/sbin/reboot
```
4.	Разрешите пользователю user4 выполнять перезагрузку ОС, но запретите завершать работу ОС.
```bash
sudo visudo
user4 ALL=(ALL) /sbin/reboot, !/sbin/shutdown
```
