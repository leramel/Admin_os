# Настраиваем
### 1. Какой порт по умолчанию использует SSH?
Порт 22 (TCP).
### 2. Можно ли изменить его? Если да — как?
Да, можно.

Открыть файл конфигурации:
```shell
   sudo nano /etc/ssh/sshd_config
```
Найти строку:
```shell
#Port 22
```
Раскомментировать и изменить номер

Сохранить файл и перезапустить службу:
```shell
sudo systemctl restart sshd
```
### 3. Какая служба отвечает за обработку входящих SSH-подключений?
Служба sshd (SSH daemon). В systemd она называется sshd.service.

### 4. Какой файл конфигурации отвечает за настройку SSH-сервера?
/etc/ssh/sshd_config

### 5. Подключитесь по SSH к предоставленному серверу.

<img width="511" height="194" alt="image" src="https://github.com/user-attachments/assets/13fe5cf4-fe23-4352-b5c4-0dd9e1767436" />

### 6. Временно разрешите подключение к серверу пользователем root, продемонстрируйте работу, а после проверки верните безопасное значение. Объясните, почему постоянный root-login нежелателен.

Редактирование файла /etc/openssh/sshd_config: добавлены директивы PermitRootLogin yes и MaxAuthTries 3. 
После перезапуска службы sshd команда sshd -T подтверждает, что настройки применились: permitrootlogin yes, maxauthtries 3.

<img width="585" height="178" alt="image" src="https://github.com/user-attachments/assets/7f76f6ba-9623-4d41-ba28-38dc8c93cc0c" />

Демонстрация подключения под пользователем root после временного разрешения PermitRootLogin yes. 
Команда whoami подтверждает, что вход выполнен от имени root. После проверки сессия завершена командой exit.

<img width="410" height="171" alt="image" src="https://github.com/user-attachments/assets/d342cacd-559a-4d8c-9322-be89b3ef8cb9" />

После возврата значения PermitRootLogin no команда sshd -T подтверждает изменение (permitrootlogin no). 
Попытка подключения под root завершается отказом: ssh: Permission denied, please try again. — вход заблокирован.

<img width="592" height="101" alt="image" src="https://github.com/user-attachments/assets/fe7ede0e-9fa3-446f-b5fe-146a6c61f2d8" />

Прямая атака брутфорсом, злоумышленники знают имя (root) и подбирают только пароль.
Нет аудита, невозможно понять, какой именно человек совершал действия.
Одна опечатка под root может сломать систему.
Лучше заходить под обычным пользователем и повышать права через sudo, которое логируется.

### 7. Измените допустимое количество ошибок аутентификации до разрыва соединения и покажите действующую настройку.

<img width="570" height="170" alt="image" src="https://github.com/user-attachments/assets/759425ba-30ec-4b5d-80b0-12e1f4a0f8f3" />

### 8. Создайте пользователя ssh-user и подключитесь им к серверу.

<img width="765" height="596" alt="image" src="https://github.com/user-attachments/assets/48c9bf1c-6cb3-4ef9-863c-fd577defd6f3" />

### 9. Ограничьте ssh-user возможность подключения к серверу.

<img width="527" height="120" alt="image" src="https://github.com/user-attachments/assets/789f810b-636c-4cdc-9455-ade34df656df" />

### 10. Покажите и объясните, как именно вы ограничили вход.
Директива DenyUsers проверяется до аутентификации. Когда клиент подключается, sshd сверяет запрашиваемое имя пользователя со списком. 
Если имя совпадает с записью в DenyUsers — соединение закрывается ещё до проверки пароля.

### 11. Что хранится в файле known_hosts?
Файл содержит публичные ключи хостов, к которым клиент уже подключался.
При первом подключении SSH спрашивает: «доверяешь ли ты этому хосту?» и сохраняет его ключ.
При повторном подключении клиент сверяет ключ сервера с сохранённым.
Если ключ не совпадает — выдаёт предупреждение:
```shell
  WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
```
### 12. Найдите ключ хоста вашего сервера в known_hosts.

<img width="1201" height="432" alt="image" src="https://github.com/user-attachments/assets/29b7d19b-9132-48a4-8b32-d860ece3b524" />

### 13. Проверьте конфигурацию sshd на ошибки до перезапуска службы.
<img width="362" height="93" alt="image" src="https://github.com/user-attachments/assets/f674bf94-42e7-4754-aba5-1a8df3afaefe" />




