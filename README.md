# Средство визуализации Grafana

Задание 1
Используя директорию help внутри этого домашнего задания, запустите связку prometheus-grafana.
Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
Подключите поднятый вами prometheus, как источник данных.
Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

![alt text](https://raw.githubusercontent.com/hawk0774/grafana1/main/Screenshot_1.png)
![alt text](https://raw.githubusercontent.com/hawk0774/grafana1/main/Screenshot_2.png)
![alt text](https://raw.githubusercontent.com/hawk0774/grafana1/main/Screenshot_3.png)

Задание 2
Изучите самостоятельно ресурсы:

PromQL tutorial for beginners and humans.
Understanding Machine CPU usage.
Introduction to PromQL, the Prometheus query language.
Создайте Dashboard и в ней создайте Panels:

утилизация CPU для nodeexporter (в процентах, 100-idle);
CPULA 1/5/15;
количество свободной оперативной памяти;
количество места на файловой системе.
Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

# CPU Utilization % (100 − idle)
100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

# Load Average 1 / 5 / 15 мин
node_load1
node_load5
node_load15

# Свободная оперативная память (в ГБ)
(node_memory_MemAvailable_bytes or (node_memory_MemFree_bytes + node_memory_Buffers_bytes + node_memory_Cached_bytes)) / 1024 / 1024 / 1024

# Свободно на дисках (ГБ) — только разделы, начинающиеся с /
node_filesystem_free_bytes{ mountpoint=~"/.*"} / 1024 / 1024 / 1024

# Общий размер разделов (ГБ) — исключаем boot, efi, snap, docker и т.п.
node_filesystem_size_bytes{ mountpoint!~"/(boot|efi|snap|var/lib/docker).*"} / 1024 / 1024 / 1024

![alt text](https://raw.githubusercontent.com/hawk0774/grafana1/main/Screenshot_4.png)

Задание 3
Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
В качестве решения задания приведите скриншот вашей итоговой Dashboard.

# Я использовал новую версию Grafana гже уже не legacy alerting, unified alerting, там можно создавать правила алертов не привязвая их к панелям дашборда.

![alt text](https://raw.githubusercontent.com/hawk0774/grafana1/main/Screenshot_5.png)

![alt text](https://raw.githubusercontent.com/hawk0774/grafana1/main/Screenshot_6.png)

![alt text](https://raw.githubusercontent.com/hawk0774/grafana1/main/Screenshot_7.png)


Задание 4
Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
В качестве решения задания приведите листинг этого файла.

