[BACK](../)

# Router

1. Перейдите "Служба" -> "Терминал" и подключаем SSH `ssh root@<ROUTER_IP>`.
2. Обновите систему `opkg update`.
3. Установка пакетов `prometheus`:

```bash
opkg install prometheus-node-exporter-lua \
  prometheus-node-exporter-lua-nat_traffic \
  prometheus-node-exporter-lua-netstat \
  prometheus-node-exporter-lua-openwrt \
  prometheus-node-exporter-lua-wifi \
  prometheus-node-exporter-lua-wifi_stations
```

4. Настройка конфига `nano /etc/config/prometheus-node-exporter-lua`:

```bash
config prometheus-node-exporter-lua 'main'
    option listen_ipv6 '0'
    option listen_port '9100'
    option listen_interface 'lan'
```

5. Перезапуск сервиса `/etc/init.d/prometheus-node-exporter-lua restart`.
6. Проверка данных:

```bash
netstat -tulpn | grep 9100

curl localhost:9100/metrics
```

7. Проверка доступа в локальной сети:

```bash
curl http://<ROUTER_IP>:9100/metrics
```

8. Обновите target в `prometheus/etc/prometheus.yml`:

```yaml
- job_name: 'openwrt-monitoring'
  scrape_interval: 30s
  static_configs:
    - targets: ['<ROUTER_IP>:9100']
```
