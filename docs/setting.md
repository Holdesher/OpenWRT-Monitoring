# Setting

1. Укажите IP-роутера в `prometheus/etc/prometheus.yml`:

```yaml
- job_name: 'openwrt-monitoring'
  scrape_interval: 30s
  static_configs:
    - targets: ['192.168.1.1:9100']
```

2. Укажите данные в `.env`:

```bash
cp .env.example .env
```

3. Запустите мониторинг:

```bash
docker compose up -d
```
