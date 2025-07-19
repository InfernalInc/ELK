# Домашнее задание к занятию "`ELK`" - `Рождественский Александр`


### Задание 1. Elasticsearch
Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный.

Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name.

### Решение 1

Что бы изменить поле `cluster_name` создал и пробросил файл [./elasticsearch/elasticsearch.yml](/elasticsearch/elasticsearch.yml) в контер

![screen](/img/1.jpg)
---

### Задание 2. Kibana
Установите и запустите Kibana.

Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty.

### Решение 2

![screen](/img/2.jpg)

---

### Задание 3. Logstash
Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch.

Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.

### Решение 3

Для настройки отправки логов использовал пайплайн [/configs/logstash/pipelines.yml](/configs/logstash/pipelines.yml), и сам конфиг [/configs/logstash/pipelines/nginx.conf](/configs/logstash/pipelines/nginx.conf).

Логи Nginx для отправки в elasticsearch пробросил в logstash и указал volume в docker compouse. 
```
    volumes:
      - ./logs:/var/log/nginx
```

![logstache](/img/3.jpg)

---

### Задание 4. Filebeat.
Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat.

Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.

### Решение 4

При написании конфига Filebeat, я сразу пробросил логи в elasticsearch, минуя Logstash. По этому в файле [/configs/filebeat/filebeat.yml](/configs/filebeat/filebeat.yml) изменен хост. Скриншот минимально информативный, потому как в Kibana не смог найти поле, где видно от куда пришли логи
```
output.elasticsearch:
  hosts: ["elasticsearch:9200"]
```
![beet](/img/4.jpg)