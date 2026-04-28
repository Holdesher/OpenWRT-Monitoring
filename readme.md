<h1 align="center">OpenWRT Monitoring</h1>

## Docs

- [Router](docs/router.md)

## Docker

```bash
# Инициализация переменных окружения
cp .env.example .env

# Запуск сервисов в фоне
docker compose up -d

# Проверка статуса контейнеров
docker compose ps

# Остановка и удаление контейнеров/сети
docker compose down
```

## Grafana

- Учетные данные задаются в `.env` (`GF_SECURITY_ADMIN_USER`, `GF_SECURITY_ADMIN_PASSWORD`).
- Дашборд подхватывается автоматически через provisioning, импорт вручную не требуется.

## Service

- Grafana: `http://localhost:3000`
- Prometheus: `http://localhost:9090`
- Targets: `http://localhost:9090/targets`
- Router target (example): `router.lan:9100`  
  При необходимости измените `prometheus/etc/prometheus.yml` под вашу сеть.

## Dashboard

- [Local](grafana/openwrt-monitoring.dashboard.json)
- [OpenWRT](https://grafana.com/grafana/dashboards/11147?spm=a2ty_o01.29997173.0.0.4ec955fbcs3wfj)
- [ASUS-OpenWRT](https://grafana.com/grafana/dashboards/18153?spm=a2ty_o01.29997173.0.0.4ec955fbcs3wfj)
