[BACK](../)

# Router

1. Перейдите "Служба" -> "Терминал" или подключитесь по SSH:

```bash
`ssh root@<ROUTER_IP>`
```

2. Обновите систему:

```bash
opkg update
```

3. Установите пакетов `prometheus`:

```bash
opkg install prometheus-node-exporter-lua \
  prometheus-node-exporter-lua-nat_traffic \
  prometheus-node-exporter-lua-netstat \
  prometheus-node-exporter-lua-openwrt \
  prometheus-node-exporter-lua-wifi \
  prometheus-node-exporter-lua-wifi_stations
```

4. Настройте конфигурацию:

```bash
nano /etc/config/prometheus-node-exporter-lua
```

```bash
config prometheus-node-exporter-lua 'main'
    option listen_ipv6 '0'
    option listen_port '9100'
    option listen_interface 'lan'
```

5. Перезапустите сервис:

```bash
/etc/init.d/prometheus-node-exporter-lua restart
```

6. Проверка доступа:

```bash
netstat -tulpn | grep 9100
```

7. Проверьте доступ в локальной сети:

```bash
curl http://<ROUTER_IP>:9100/metrics
```

8. Укажите IP-роутера в `prometheus/etc/prometheus.yml`:

```yaml
- job_name: 'openwrt-monitoring'
  scrape_interval: 30s
  static_configs:
    - targets: ['<ROUTER_IP>:9100']
```
