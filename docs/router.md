[BACK](../)

# Router

## Setup

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
opkg install prometheus-node-exporter-lua prometheus-node-exporter-lua-nat_traffic prometheus-node-exporter-lua-netstat prometheus-node-exporter-lua-openwrt prometheus-node-exporter-lua-wifi prometheus-node-exporter-lua-wifi_stations
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

## Addons

- Ошибка связанная с `uhttpd_lua`, можно исправить:

```bash
opkg update
opkg install uhttpd-mod-lua lua
```

```bash
/etc/init.d/uhttpd restart
/etc/init.d/prometheus-node-exporter-lua restart
```

## Checker

- Проверка доступа:

```bash
netstat -tulpn | grep 9100
```

- Просмотр логов:

```bash
logread | tail -n 120
```

- Проверьте доступ в локальной сети:

```bash
curl http://<ROUTER_IP>:9100/metrics
```
