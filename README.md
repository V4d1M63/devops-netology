## Домашнее задание к занятию "13.Системы мониторинга" - Вдовин Вадим

### Обязательные задания

1. Вас пригласили настроить мониторинг на проект. На онбординге вам рассказали, что проект представляет из себя платформу для вычислений с выдачей текстовых отчетов, которые сохраняются на диск. Взаимодействие с платформой осуществляется по протоколу http. Также вам отметили, что вычисления загружают ЦПУ. Какой минимальный набор метрик вы выведите в мониторинг и почему?

Ответ: 

- CPU Utilization (Использование ЦПУ):

Это ключевая метрика, так как вы говорите о вычислениях, которые загружают ЦПУ. 

- Память (RAM) Utilization (Использование памяти):

Мониторинг использования оперативной памяти важен для определения, не исчерпана ли память, что может привести к снижению производительности или даже к падению системы.

- Использование диска (Disk Utilization):

Отслеживание использования дискового пространства может помочь предотвратить переполнение диска и потерю данных.

- Загрузка сети (Network Throughput):

Если взаимодействие с платформой осуществляется по протоколу HTTP, следите за объемом сетевого трафика, чтобы убедиться, что сеть не является узким местом.

- Логи ошибок (Error Logs):

Отслеживание ошибок и исключений в логах помогает выявить и решить проблемы в системе.

- Метрики доступности (Availability Metrics):

Мониторинг доступности платформы важен для обеспечения ее надежной работы. Это может включать в себя проверку статуса серверов и уведомления в случае отказа.

2. Менеджер продукта посмотрев на ваши метрики сказал, что ему непонятно что такое RAM/inodes/CPUla. Также он сказал, что хочет понимать, насколько мы выполняем свои обязанности перед клиентами и какое качество обслуживания. Что вы можете ему предложить?

- RAM (Random Access Memory) - объем оперативной памяти, используемый сервером или приложением.
- Inodes - структуры данных в файловой системе, которые отслеживают информацию о файлах и каталогах.
- CPUla (CPU Load Average) - средняя нагрузка на процессор системы.

Метрики берем из приложения или БД.

3. Вашей DevOps команде в этом году не выделили финансирование на построение системы сбора логов. Разработчики в свою очередь хотят видеть все ошибки, которые выдают их приложения. Какое решение вы можете предпринять в этой ситуации, чтобы разработчики получали ошибки приложения?

- Используйте бесплатные или открытые инструменты для сбора и анализа логов, такие как Elasticsearch, Logstash и Kibana (ELK Stack) или Fluentd и Grafana. Эти инструменты могут предоставить базовую функциональность сбора и анализа логов без значительных затрат.

4. Вы, как опытный SRE, сделали мониторинг, куда вывели отображения выполнения SLA=99% по http кодам ответов. Вычисляете этот параметр по следующей формуле: summ_2xx_requests/summ_all_requests. Данный параметр не поднимается выше 70%, но при этом в вашей системе нет кодов ответа 5xx и 4xx. Где у вас ошибка?

- В данном случае, формула summ_2xx_requests/summ_all_requests оценивает только процент успешных запросов (HTTP 2xx). Она не учитывает другие коды ответов, такие как 3xx (перенаправления) и 1xx (информационные ответы).

Для вычисления общего SLA, включая все категории кодов ответов, следует использовать следующую формулу:

SLA = (summ_2xx_requests + summ_3xx_requests + summ_1xx_requests) / summ_all_requests

5. Опишите основные плюсы и минусы pull и push систем мониторинга.

### Pull системы мониторинга:

Плюсы:

- Сниженная нагрузка на целевые системы: В pull-системах мониторинга, мониторинговые агенты (клиенты) опрашивают целевые системы (серверы) по запросу, что позволяет более точно контролировать частоту опроса и снижает нагрузку на целевые системы. Это особенно полезно для высоконагруженных приложений.

- Более простая настройка и установка: Pull-системы часто проще настраивать и устанавливать, так как агенты мониторинга могут быть легко развернуты на целевых серверах без дополнительных настроек на стороне сервера.

- Прозрачность для целевых систем: Целевые системы могут быть неосведомленными о наличии мониторинга и агентов, что может быть полезно в некоторых ситуациях для соблюдения конфиденциальности.

Минусы:

- Задержка в обновлении данных: Поскольку мониторинговые агенты опрашивают целевые системы по расписанию, существует задержка в обновлении данных. Это может снизить способность обнаружения проблем в режиме реального времени.

- Потеря данных: Если агент неспособен опросить целевую систему (например, из-за сетевой проблемы или сбоя агента), это может привести к потере данных мониторинга.

### Push системы мониторинга:

Плюсы:

- Реальное время: Push-системы мониторинга позволяют отправлять данные в реальном времени, что делает их более подходящими для мониторинга важных событий и реагирования на них мгновенно.

- Легкость настройки центрального сервера: В push-системах, центральный сервер (коллектор данных) более централизован и может быть легче настроен для обработки данных от множества клиентских систем.

- Уведомления в режиме реального времени: Push-системы могут легко отправлять уведомления и события в реальном времени на основе данных мониторинга.

Минусы:

- Высокая нагрузка на целевые системы: При использовании push-систем могут возникнуть проблемы с нагрузкой на целевые системы, особенно если большое количество данных отправляется в реальном времени.

- Сложность настройки агентов: Настройка и установка агентов на целевых серверах может быть более сложной и требовательной к ресурсам процедурой.

- Безопасность и приватность: Push-системы требуют от целевых систем предоставлять доступ для приема данных мониторинга, что может повысить риски вопросов безопасности и приватности.

6. Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?

- Prometheus - pull.
- TICK - push.
- Zabbix - pull, push.
- VictoriaMetrics - push.
- Nagios - pull.

7. Склонируйте себе репозиторий и запустите TICK-стэк, используя технологии docker и docker-compose.
В виде решения на это упражнение приведите скриншот веб-интерфейса ПО chronograf (http://localhost:8888).

P.S.: если при запуске некоторые контейнеры будут падать с ошибкой - проставьте им режим Z, например ./data:/var/lib:Z

8. Перейдите в веб-интерфейс Chronograf (http://localhost:8888) и откройте вкладку Data explorer.

- Нажмите на кнопку Add a query
- Изучите вывод интерфейса и выберите БД telegraf.autogen
- В measurments выберите cpu->host->telegraf-getting-started, а в fields выберите usage_system. Внизу появится график утилизации cpu.
- Вверху вы можете увидеть запрос, аналогичный SQL-синтаксису. Поэкспериментируйте с запросом, попробуйте изменить группировку и интервал наблюдений.

Для выполнения задания приведите скриншот с отображением метрик утилизации cpu из веб-интерфейса.

![1](https://github.com/V4d1M63/devops-netology/assets/130470784/b58d46d4-2855-4387-b17b-7a63e8242cfc)

9. Изучите список telegraf inputs. Добавьте в конфигурацию telegraf следующий плагин - docker:

```
[[inputs.docker]]
  endpoint = "unix:///var/run/docker.sock"
```  

Дополнительно вам может потребоваться донастройка контейнера telegraf в docker-compose.yml дополнительного volume и режима privileged:
```
  telegraf:
    image: telegraf:1.4.0
    privileged: true
    volumes:
      - ./etc/telegraf.conf:/etc/telegraf/telegraf.conf:Z
      - /var/run/docker.sock:/var/run/docker.sock:Z
    links:
      - influxdb
    ports:
      - "8092:8092/udp"
      - "8094:8094"
      - "8125:8125/udp"
```
После настройке перезапустите telegraf, обновите веб интерфейс и приведите скриншотом список measurments в веб-интерфейсе базы telegraf.autogen . Там должны появиться метрики, связанные с docker.

Приводим настройки контейнера telegraf к следующему виду:

```
  telegraf:
    # Full tag list: https://hub.docker.com/r/library/telegraf/tags/
    build:
      context: ./images/telegraf/
      dockerfile: ./${TYPE}/Dockerfile
      args:
        TELEGRAF_TAG: ${TELEGRAF_TAG}
    image: "telegraf"
    user: telegraf:997
    environment:
      HOSTNAME: "telegraf-getting-started"
    # Telegraf requires network access to InfluxDB
    links:
      - influxdb
    volumes:
      # Mount for telegraf configuration
      - ./telegraf/:/etc/telegraf/
      # Mount for Docker API access
      - /var/run/docker.sock:/var/run/docker.sock
    depends_on:
      - influxdb
```
в конфигурации telegraf плагин docker существует

![2](https://github.com/V4d1M63/devops-netology/assets/130470784/f48639d2-257d-4f85-b239-e59b62f67ecc)
