# Отчет по заданию PROM FINAL

На node1 установил docker и docker compose из официальных пакетов.
Wordpress запустил через приведенный docker-compose.yml

## Cadvisor

Cadvisor скачал из репозитория https://github.com/google/cadvisor , запустил как systemd unit, отдельного пользователя не создавал.
```
[Unit]
Description=Cadvisor is a running daemon that collects, aggregates, processes, and exports information about running containers
After=network.target
Wants=network-online.target

[Service]
User=root
Group=root
Type=simple
ExecStart=/opt/cadvisor/cadvisor

[Install]
WantedBy=multi-user.target
```

Логи запуска (не особо много):
```
-- Logs begin at Wed 2023-06-14 06:14:21 UTC, end at Wed 2023-06-14 07:41:57 UTC. --
Jun 14 06:17:06 node1 systemd[1]: Started Cadvisor is a running daemon that collects, aggregates, processes, and exports information about running containers.
```

## Node Exporter

Node exporter скачал с сайта prometheus: https://prometheus.io/download/#node_exporter , запустил как systemd unit, отдельного пользователя не создавал.
```
[Unit]
Description=Node Exporter
After=network.target
Wants=network-online.target

[Service]
User=root
Group=root
Type=simple
ExecStart=/opt/node_exporter/node_exporter

Restart=always
RestartSec=1
StartLimitInterval=0

[Install]
WantedBy=multi-user.target
```

Логи запуска:
```
-- Logs begin at Wed 2023-06-14 06:14:21 UTC, end at Wed 2023-06-14 07:41:57 UTC. --
Jun 14 06:17:09 node1 systemd[1]: Started Node Exporter.
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.279Z caller=node_exporter.go:180 level=info msg="Starting node_exporter" version="(version=1.6.0, branch=HEAD, revision=ff7f9d69b645cb691dd3e84dc3af>
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.281Z caller=node_exporter.go:181 level=info msg="Build context" build_context="(go=go1.20.4, platform=linux/amd64, user=root@f9c3ed0cfbd3, date=2023>
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.282Z caller=node_exporter.go:183 level=warn msg="Node Exporter is running as root user. This exporter is designed to run as unprivileged user, root >
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.289Z caller=filesystem_common.go:111 level=info collector=filesystem msg="Parsed flag --collector.filesystem.mount-points-exclude" flag=^/(dev|proc|>
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.290Z caller=filesystem_common.go:113 level=info collector=filesystem msg="Parsed flag --collector.filesystem.fs-types-exclude" flag=^(autofs|binfmt_>
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.293Z caller=diskstats_common.go:111 level=info collector=diskstats msg="Parsed flag --collector.diskstats.device-exclude" flag=^(ram|loop|fd|(h|s|v|>
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.294Z caller=node_exporter.go:110 level=info msg="Enabled collectors"
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.294Z caller=node_exporter.go:117 level=info collector=arp
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.294Z caller=node_exporter.go:117 level=info collector=bcache
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.294Z caller=node_exporter.go:117 level=info collector=bonding
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.294Z caller=node_exporter.go:117 level=info collector=btrfs
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.295Z caller=node_exporter.go:117 level=info collector=conntrack
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.295Z caller=node_exporter.go:117 level=info collector=cpu
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.295Z caller=node_exporter.go:117 level=info collector=cpufreq
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.295Z caller=node_exporter.go:117 level=info collector=diskstats
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.297Z caller=node_exporter.go:117 level=info collector=dmi
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.297Z caller=node_exporter.go:117 level=info collector=edac
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.297Z caller=node_exporter.go:117 level=info collector=entropy
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.297Z caller=node_exporter.go:117 level=info collector=fibrechannel
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.297Z caller=node_exporter.go:117 level=info collector=filefd
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.297Z caller=node_exporter.go:117 level=info collector=filesystem
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=hwmon
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=infiniband
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=ipvs
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=loadavg
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=mdadm
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=meminfo
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=netclass
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.298Z caller=node_exporter.go:117 level=info collector=netdev
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=netstat
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=nfs
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=nfsd
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=nvme
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=os
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=powersupplyclass
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=pressure
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.299Z caller=node_exporter.go:117 level=info collector=rapl
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=schedstat
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=selinux
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=sockstat
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=softnet
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=stat
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=tapestats
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=textfile
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.300Z caller=node_exporter.go:117 level=info collector=thermal_zone
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.301Z caller=node_exporter.go:117 level=info collector=time
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.301Z caller=node_exporter.go:117 level=info collector=timex
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.301Z caller=node_exporter.go:117 level=info collector=udp_queues
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.301Z caller=node_exporter.go:117 level=info collector=uname
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.301Z caller=node_exporter.go:117 level=info collector=vmstat
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.301Z caller=node_exporter.go:117 level=info collector=xfs
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.305Z caller=node_exporter.go:117 level=info collector=zfs
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.309Z caller=tls_config.go:274 level=info msg="Listening on" address=[::]:9100
Jun 14 06:17:09 node1 node_exporter[38997]: ts=2023-06-14T06:17:09.313Z caller=tls_config.go:277 level=info msg="TLS is disabled." http2=false address=[::]:9100
```

## Mysqld Exporter

Mysqld exporter скачал из репозитория https://github.com/prometheus/mysqld_exporter , запустил в контейнере вместе с wordpress:
```
version: "3.8"

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_USER: "root"
      MYSQL_ROOT_PASSWORD: "12345678"
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: "87654321"

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: "87654321"
      WORDPRESS_DB_NAME: wordpress

  exporter:
    depends_on:
    - db
    image: prom/mysqld-exporter
    volumes:
    - ./my.cnf:/my.cnf
    ports:
    - "9104:9104"
    command:
    - "--config.my-cnf=/my.cnf"

volumes:
  db_data: {}
  wordpress_data: {}
  my.cnf:
```
Данные для подключения к базе (my.cnf):
```
[client]
host=db
port=3306
user=root
password=12345678
```

Логи запуска:
```
root@node1:/opt/wordpress# docker logs fc73a544bc93
ts=2023-06-14T06:29:36.920Z caller=mysqld_exporter.go:277 level=info msg="Starting mysqld_exporter" version="(version=0.14.0, branch=HEAD, revision=ca1b9af82a471c849c529eb8aadb1aac73e7b68c)"
ts=2023-06-14T06:29:36.921Z caller=mysqld_exporter.go:278 level=info msg="Build context" (gogo1.17.8,userroot@401d370ca42e,date20220304-16:25:15)=(MISSING)
ts=2023-06-14T06:29:36.921Z caller=mysqld_exporter.go:293 level=info msg="Scraper enabled" scraper=global_status
ts=2023-06-14T06:29:36.921Z caller=mysqld_exporter.go:293 level=info msg="Scraper enabled" scraper=global_variables
ts=2023-06-14T06:29:36.921Z caller=mysqld_exporter.go:293 level=info msg="Scraper enabled" scraper=slave_status
ts=2023-06-14T06:29:36.921Z caller=mysqld_exporter.go:293 level=info msg="Scraper enabled" scraper=info_schema.innodb_cmp
ts=2023-06-14T06:29:36.922Z caller=mysqld_exporter.go:293 level=info msg="Scraper enabled" scraper=info_schema.innodb_cmpmem
ts=2023-06-14T06:29:36.922Z caller=mysqld_exporter.go:293 level=info msg="Scraper enabled" scraper=info_schema.query_response_time
ts=2023-06-14T06:29:36.922Z caller=mysqld_exporter.go:303 level=info msg="Listening on address" address=:9104
ts=2023-06-14T06:29:36.925Z caller=tls_config.go:195 level=info msg="TLS is disabled." http2=false
```

## Prometheus

Prometheus скачал с сайта https://prometheus.io/download/#prometheus , установил как systemd unit:
```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=root
Group=root
Type=simple
ExecStart=/opt/prometheus/prometheus \
    --config.file=/opt/prometheus/prometheus.yml \
    --storage.tsdb.path=/opt/prometheus/data \
    --web.console.templates=/opt/prometheus/consoles \
    --web.console.libraries=/opt/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```

В конфигурацию добавил таргеты на установленные экспортеры:
```
.....
  - job_name: "node"
    static_configs:
    - targets: ["64.227.77.41:9100"]

  - job_name: "docker"
    static_configs:
    - targets: ["64.227.77.41:8080"]

  - job_name: "mysql"
    static_configs:
    - targets: ["64.227.77.41:9104"]
```

## Grafana

Установил графану из пакета: https://grafana.com/grafana/download/9.5.3?edition=oss
Подключил Datasource Prometheus.
Импортировал дашборды:
- для Cadvisor: https://grafana.com/grafana/dashboards/14282-cadvisor-exporter/
- для Node exporter: https://grafana.com/grafana/dashboards/1860-node-exporter-full/
- для Mysqld exporter: https://grafana.com/grafana/dashboards/11323-mysql/

### Скриншоты дашбордов
![image](https://github.com/aglumov/rebrain_prom_final/assets/91331755/13e4158d-9a64-4538-abb6-d3cd1133ec61)
![image](https://github.com/aglumov/rebrain_prom_final/assets/91331755/1ccb0ab2-5c4e-47a5-bfae-e02e01d31190)
![image](https://github.com/aglumov/rebrain_prom_final/assets/91331755/2ef04185-7477-47e8-a1d0-c30225d8f62f)



