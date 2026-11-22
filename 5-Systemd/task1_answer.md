# Юниты

### 1. Что такое systemd unit?
Systemd unit (юнит) — это базовый объект, которым управляет systemd. Это конфигурационный файл с расширением 
(например, .service, .timer, .socket, .mount), который описывает ресурс, службу или точку монтирования, 
а также правила их работы в системе.

### 2. Проверьте статус любого systemd unit. Какую информацию выводит эта команда?
```shell
systemctl status crond

<img width="833" height="235" alt="image" src="https://github.com/user-attachments/assets/869402e1-1762-4d57-b60b-93daa1d205c3" />


```
* Loaded: Путь к файлу юнита и статус автозагрузки (enabled или disabled).
* Active: Текущее состояние (active (running) или inactive (dead)), а также время, прошедшее с момента запуска.
* Main PID: Идентификатор главного процесса службы.
* Tasks / Memory: Количество потоков и объем потребляемой оперативной памяти.
* CGroup: Иерархия процессов, относящихся к этому юниту.
* Журнал (Logs): Последние 10-15 строк логов этой службы, что критически важно для диагностики.

### 3. Остановите выбранный сервис.
```shell
sudo systemctl stop crond
```

### 4. Запустите его снова.
```shell
sudo systemctl start crond
```

<img width="833" height="643" alt="image" src="https://github.com/user-attachments/assets/714ba797-80d6-4d71-84c8-288b64d3f44f" />


### 5. Уберите сервис из автозагрузки.
```shell
sudo systemctl disable crond
```

### 6. Верните его в автозагрузку.
```shell
sudo systemctl enable crond
```

<img width="1029" height="335" alt="image" src="https://github.com/user-attachments/assets/8651faa1-614e-4284-ae90-cd8afc888b47" />

### 7. Чем отличаются состояния active, enabled, disabled, failed?

1) active - Служба запущена и работает прямо сейчас.
2) inactive - Служба остановлена прямо сейчас.
3) enabled - Служба будет запущена автоматически при следующей загрузке системы.
4) disabled - Служба не будет запущена автоматически при загрузке (но её можно запустить вручную).
5) failed - Служба попыталась запуститься, но завершилась с ошибкой.

### 8. Что такое systemd timers?
Это механизм планирования задач, альтернатива классическому cron. 
Таймеры (.timer) запускают соответствующие юниты по расписанию.
Преимущества перед cron: интеграция с журналом systemd (journalctl), 
возможность запускать задачи относительно событий (например, через 5 минут после загрузки).

### 9. Найдите хотя бы один существующий timer в системе и определите, какой unit он запускает.
Список всех таймеров в системе:
```shell
systemctl list-timers --all
```
<img width="1057" height="553" alt="image" src="https://github.com/user-attachments/assets/d4823dcf-4ddd-432f-9495-cf33e1dcb398" />


Таймер logrotate.timer запускает сервис logrotate.service.
















