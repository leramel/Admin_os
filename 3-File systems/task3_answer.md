# Файловые системы. Продолжение
### 1. Выведите содержимое /etc/fstab. Что хранится в этом файле?
```shell
cat /etc/fstab
```

/etc/fstab (file systems table) — это конфигурационный файл, который содержит информацию о файловых системах, которые должны быть автоматически смонтированы при загрузке системы.
Формат строки
```shell
<устройство>  <точка_монтирования>  <тип_ФС>  <параметры>  <dump>  <pass>
```
Поля:
1) Устройство — UUID, LABEL или имя устройства (например, /dev/sda1)
2) Точка монтирования — каталог, куда будет смонтирована ФС (например, /, /home, /mnt/data)
3) Тип файловой системы — ext4, xfs, vfat, swap и т.д.
4) Параметры монтирования — defaults, ro (только чтение), noexec, nosuid и др.
5) dump — флаг для утилиты backup (обычно 0)
6) pass — порядок проверки fsck при загрузке (0 — не проверять, 1 — для корня, 2 — для остальных)

<img width="987" height="244" alt="image" src="https://github.com/user-attachments/assets/fcffc56a-f20c-402d-86e2-7ee994391aae" />

### 2. Добавьте в виртуальную машину еще один виртуальный диск.
<img width="409" height="281" alt="image" src="https://github.com/user-attachments/assets/42e86d8c-ad2d-432c-84ae-1435147b3465" />

### 3. Определите, как система видит новый диск, и выведите информацию о блочных устройствах.
<img width="438" height="155" alt="image" src="https://github.com/user-attachments/assets/9ba7adc1-5819-4b8e-9a96-d377d4790c7a" />

<img width="676" height="714" alt="image" src="https://github.com/user-attachments/assets/6e9360dd-81c8-4c58-8f0f-5a2136813388" />

sdb — новый диск (5 ГБ)

### 4. Создайте на новом диске таблицу разделов и один раздел.

1) o — создать новую пустую таблицу разделов DOS (MBR)
2) n — создать новый раздел
3) p — выбрать основной раздел (primary)
4) 1 — номер раздела (1)
5) Enter — принять первый сектор по умолчанию
6) Enter — принять последний сектор по умолчанию (использовать весь диск)
7) w — записать изменения и выйти

<img width="791" height="686" alt="image" src="https://github.com/user-attachments/assets/5a9e0dd7-24b9-471f-bc09-5f9eb79bf282" />

### 5. Создайте на разделе файловую систему ext4.

<img width="688" height="320" alt="image" src="https://github.com/user-attachments/assets/1aea2554-379d-4d74-a3c8-f038396d412c" />

### 6. Создайте отдельный каталог в /mnt и подключите к нему файловую систему.

<img width="649" height="135" alt="image" src="https://github.com/user-attachments/assets/d91a8008-9f66-4bd2-827e-4c746ae6a1df" />

### 7. Создайте на подключенном диске несколько файлов.

<img width="727" height="243" alt="image" src="https://github.com/user-attachments/assets/e9354ce1-356d-433d-bb38-bacfd765acc4" />

### 8. Отключите диск и проверьте, видны ли созданные файлы через каталог монтирования. Объясните результат.

<img width="418" height="86" alt="image" src="https://github.com/user-attachments/assets/4634fd8b-686d-4232-bad8-481f7475ce0c" />

Когда мы размонтировали файловую систему, каталог /mnt/data вернулся в своё исходное состояние — это просто пустая папка в корневой файловой системе. 
Файлы, которые мы создавали, физически находятся на диске /dev/sdb1, но они недоступны, пока файловая система не смонтирована обратно.
Если монтировать обратно, то файлы снова появятся. Они не удалились, а были отключены вместе с файловой системой.

### 9. Настройте автоматическое монтирование файловой системы при загрузке через /etc/fstab.

<img width="1029" height="188" alt="image" src="https://github.com/user-attachments/assets/7051a51e-d95f-43bd-8ef9-3cbff0c6dec5" />

### 10. Для записи в /etc/fstab используйте UUID файловой системы, а не имя вида /dev/sdX.
Хорошо
### 11. Проверьте корректность /etc/fstab до перезагрузки.
<img width="668" height="129" alt="image" src="https://github.com/user-attachments/assets/8549de4d-2093-4d50-9873-d4bacaffe699" />

Команда выполнилась без ошибок, значит, запись в /etc/fstab корректна.

### 12. Перезагрузите систему и убедитесь, что файловая система монтируется автоматически.

```shell
sudo reboot - перезагрузка
```
<img width="687" height="259" alt="image" src="https://github.com/user-attachments/assets/64786373-b631-4321-8dc5-36635284efba" />

