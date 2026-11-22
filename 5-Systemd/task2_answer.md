# Пишем юниты

### 1. Создайте скрипт, который создаёт каталог и четыре файла с именами 1, 2, 3, 4. В файлы запишите соответственно:

текущую дату;
версию ядра;
имя компьютера;
список файлов в домашнем каталоге пользователя, от которого выполняется скрипт. Не забудьте проверять существование каталогов и файлов.

<img width="681" height="759" alt="image" src="https://github.com/user-attachments/assets/88086717-438a-4171-8980-22f78a6e622a" />

### 2. Создайте systemd service, который запускает этот скрипт. Проверьте его работу.

<img width="971" height="466" alt="image" src="https://github.com/user-attachments/assets/10ef2e31-c394-4c01-9a20-77b2ec83a8a3" />

### 3. Создайте timer, который запускает этот service каждые 5 минут.

<img width="1116" height="478" alt="image" src="https://github.com/user-attachments/assets/38107a94-be88-44c2-8e2b-f9190b1e4cfb" />

### 4. От какого пользователя по умолчанию выполняются системные units?
По умолчанию выполняются от root

### 5. Создайте отдельного пользователя для выполнения вашего скрипта.

<img width="849" height="743" alt="image" src="https://github.com/user-attachments/assets/8171eb05-af84-4e21-bd44-f7fcafda7094" />

### 6. Дополните unit так, чтобы скрипт выполнялся от созданного пользователя.

<img width="1046" height="805" alt="image" src="https://github.com/user-attachments/assets/27a88c40-69b7-46d2-b5cb-8c620d6d5933" />

После добавления User=scriptuser и Group=scriptuser в unit-файл, сервис выполняется от имени пользователя scriptuser. 

Файлы создаются в его домашнем каталоге /home/scriptuser/myinfo_output/. Статус сервиса после выполнения — inactive (dead)

### 7. Дополните скрипт так, чтобы он независимо от текущего каталога выполнял работу в домашнем каталоге пользователя, от которого запущен.

<img width="781" height="341" alt="image" src="https://github.com/user-attachments/assets/fe5d9618-8d6b-4483-999b-d44be7231b42" />

### 8. Определите PID процесса во время выполнения, если он успевает существовать достаточно долго.

```shell
myinfo.sh[4277]   ← PID = 4277
myinfo.sh[4292]   ← PID = 4292
myinfo.sh[4315]   ← PID = 4315
```
Каждый запуск сервиса создаёт новый процесс со своим уникальным PID

<img width="1019" height="612" alt="image" src="https://github.com/user-attachments/assets/1f3d1092-9f3e-47a0-8db4-b2c830afbd2c" />

### 9. Найдите в journal записи о запуске service.

<img width="1053" height="581" alt="image" src="https://github.com/user-attachments/assets/952d6662-c9cf-4493-aaa7-47eb4f8e9682" />

### 10. Намеренно внесите ошибку в скрипт или unit, добейтесь состояния failed, определите причину через systemctl и journalctl, затем исправьте.
Ошибка несуществующего файла

<img width="1025" height="576" alt="image" src="https://github.com/user-attachments/assets/375f678f-7e37-4df4-8ec8-4075e3a01975" />

Диагностика через journalctl
```shell
sudo journalctl -u myinfo.service -n 10

myinfo.service: Failed with result 'exit-code'.
Failed to start myinfo.service
```

<img width="975" height="104" alt="image" src="https://github.com/user-attachments/assets/58df9d84-2ec5-4216-8b63-9960b8914ebe" />

Диагностика через systemctl
```shell
systemctl show myinfo.service | grep -E 'Result|ExitStatus|ExecMainStatus'

Result=exit-code
ExecMainStatus=1
```

<img width="1003" height="259" alt="image" src="https://github.com/user-attachments/assets/327c4919-b520-482b-b823-1a2aef5fc792" />


Исправляем
```shell
Main PID: 4422 (code=exited, status=0/SUCCESS)
```
<img width="1038" height="760" alt="image" src="https://github.com/user-attachments/assets/d870d1a8-e969-4aa0-bdc0-afb188528d08" />






