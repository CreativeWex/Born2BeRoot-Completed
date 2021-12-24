# Born 2beRoot
Основные команды
- Ребут `sudo reboot`


# Mandatory part
~~Разобраться с политикой паролей~~
~~- Вопрос о снапшотах~~
- ОБНОВИТЬ ПАРОЛИ

- Код скрипта разобрать

~~- Файл Руслана, проделать Tips~~

~~- Как прекратить исполнение скрипта~~

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

### Политика паролей
Конфиг `nano /etc/pam.d/common-password`

Дописываем строку следующим образом:
`password requisite pam_pwquality.so minlen=10 ucredit=-1 lcredit=-1
dcredit=-1 maxrepeat=3 retry=3`

`usercheck=1 enforce_for_root` правила для root

<br>
<br>
`password requisite pam_pwquality.so minlen=10 ucredit=-1 lcredit=-1
dcredit=-1 maxrepeat=3 retry=3 usercheck=1 difok=7` правила для всех users

остановился пока на этом.

# Script

Awk - сканирует входной файл в поисках шаблонов

1) [Architecture] `wall` - пишет сообщение, `uname -a` - выводит информацию  системе, `wc -l` - выводит все строки(количество)

2,3) [CPU physical] `cat /proc/cpuinfo` выводит всю информацию о всех процессорах, `grep` - ищет первое вхождение, затем печатает на экран, `wc -l` - выводит количество строк

4) [Memory Usage] `free -m` - отображает количество свободной и использованной памяти(Гб), `NR==2` - номер текущей записи в общем входном потоке
5) [Disk usage] `df -h ` - инфа по использованию диска в разрядности 1024. `NF` - число полей в текущем инпуте
6) [CPU Load] `top -bn1` - отображает процессы linux (b передает output из top в программы/файл работает до предела итераций n)
7) [Last boot] `who` - показывает залогиненых `-b` - показывает последний бут
8) [LVM Use] 
9) [Connection TCP] - `netstat` - отображает все, что связано с соединениями `-a` - все сокеты `-n` - число портов
10) [User log] - `cut` выводит выбранные части строк, `-d` - задает разделитель, `-f` = СПИСОК (выводит только столбцы, пперечисленные в списке), `sort` - сортирует строки `-u` строки не повторяются(уникальные)
11) [Network IP] `hostname` - имя хоста, `-I` - все сетевые адреса хоста




