# Домашнее задание к занятию «Prometheus. Часть 2»

### Задание 1
Создайте файл с правилом оповещения, как в лекции, и добавьте его в конфиг Prometheus.

### Требования к результату
- [ ] Погасите node exporter, стоящий на мониторинге, и прикрепите скриншот раздела оповещений Prometheus, где оповещение будет в статусе Pending

### Решение
1. качаем пакет https://github.com/prometheus/alertmanager/releases/download/v0.28.0-rc.0/alertmanager-0.28.0-rc.0.linux-amd64.tar.gz
2. извлекаем tar -xvf alertmanager-0.28.0-rc.0.linux-amd64.tar.gz
3. копируем файл в папку cp ./alertmanager-0.28.0-rc.0.linux-amd64/alertmanager /usr/local/bin/
4. копируем файл в папку cp ./alertmanager-0.28.0-rc.0.linux-amd64/amtool /usr/local/bin/
5. копируем файл в папку cp ./alertmanager-0.28.0-rc.0.linux-amd64/alertmanager.yml /etc/prometheus/
6. даем права пользователю прометеус chown prometheus:prometheus /etc/prometheus/alertmanager.yml
7. делаем его доступным для systemctl, создаем сервис nano /etc/systemd/system/prometheus-alertmanager.service
Вставляем параметры
```ini
[Unit]

Description=Alertmanager Service

After=network.target

[Service]

EnvironmentFile=-/etc/default/alertmanager

User=prometheus

Group=prometheus

Type=simple

ExecStart=/usr/local/bin/alertmanager --config.file=/etc/prometheus/alertmanager.yml
--storage.path=/var/lib/prometheus/alertmanager $ARGS

ExecReload=/bin/kill -HUP $MAINPID

Restart=on-failure

[Install]

WantedBy=multi-user.target
```
8. Включаем автозапуск sudo systemctl enable prometheus-alertmanager.service
9. запускаем и смотрим статус sudo systemctl start  prometheus-alertmanager.service
10. udo systemctl status  prometheus-alertmanager.service
---

### Задание 2
Установите Alertmanager и интегрируйте его с Prometheus.

### Требования к результату
- [ ] Прикрепите скриншот Alerts из Prometheus, где правило оповещения будет в статусе Fireing, и скриншот из Alertmanager, где будет видно действующее правило оповещения

---

### Задание 3

Активируйте экспортёр метрик в Docker и подключите его к Prometheus.

### Требования к результату
- [ ] приложите скриншот браузера с открытым эндпоинтом, а также скриншот списка таргетов из интерфейса Prometheus.*

---

### Задание 4* (со звездочкой)

Создайте свой дашборд Grafana с различными метриками Docker и сервера, на котором он стоит.


