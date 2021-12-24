# Born 2beRoot
Основные команды
- Ребут `sudo reboot`


# Mandatory part
- Разобраться с политикой паролей
- Вопрос о снапшотах
- Код скрипта разобрать
- Файл Руслана, проделать Tips
- Как прекратить исполнение скрипта

## Теория
- Работа виртуальной машины
- Выбор ОС, разница между дебиан и центт
- Предназначение виртуальной машины
- Определения aptitude, apt, APPARmor
- Инфа про разбиение на логические тома
- sudo
## Simple setup
- !!!!!!!!! обратить внимание на пароли !!!!!!!!!

- убеждаемся, файрвол работает
`sudo ufw status`
-  ssh работает
`systemctl status ssh`

## User

- посмотреть всех пользователей
`sudo cut -d: -f1 /etc/passwd`

- посмотреть в каких группах состоит пользователь
`id -Gn <user>`
- создать пользователя с папкой / без папки (С ПАРОЛЕМ )
`sudo adduser <user>` / `sudo useradd <user>`

Правила по заполнению паролей `nano /etc/login.defs`

Конфиг правила паролей `nano /etc/pam.d/common-password`

- создать группу `groupadd <you_group>`
- посмотреть группы `getent group`
- добаваить пользователя в группу `usermod -aG <you_group> <you_user>`
- удалить пользователя из группы `gpasswd -d <you_user> <you_group>`

## Hostname and partisions
- смена имени хоста
`nano /etc/hosts` и `nano /etc/hostname`
- Партиции `lsblk`
- инфа про лвм

## Sudo

- проверка наличия пакетов `sudo apt install sudo`
- лог судо `/var/log/sudo/`

## UFW

- проверка, что работает `sudo ufw status numbered`
- добавить порт `sudo ufw allow 8080`
- удалить порт `sudo ufw delete`

## SSH
- ssh работает `systemctl status ssh`
- ssh определение
- проверка что порт 4242 `nano /etc/ssh/sshd_config`
- подключиться через ssh к машине `ssh user@localhost -p 4242`

## Script Monitoring
Проходим по пути `cd /usr/local/bin/`

- Скрипт `touch monitoring.sh`
- Определение Cron
- Правило для скрипта без пароля `sudo visudo`
- Открытие крон таба для отложенного запуска скрипта `sudo crontab -u root -e`

### Скрипт на 10 минут

``sudo crontab -u root -e``

### Скрипт на 30 секунд

``#* * * * * /usr/local/bin/monitoring.sh``

``#* * * * * ( sleep 30 ; /usr/local/bin/monitoring.sh )``
