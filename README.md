# Cosmos Chains Dashboard

A [Grafana](https://grafana.com/) dashboard compatible with all the [cosmos-sdk](https://github.com/cosmos/cosmos-sdk) and [tendermint](https://github.com/tendermint/tendermint) based blockchains.

## Preview

![1](imgs/cosmos-overview.jpg)
![2](imgs/irishub-overview.jpg)
![3](imgs/instance-overview.jpg)

## How To

We assume that you already have [Grafana](https://grafana.com/) and [Prometheus](https://prometheus.io/) installed.

### Enable Tendermint Metrics

```bash
sed -i 's/prometheus = false/prometheus = true/g' <YOUR-NODE-HOMEDIR>/config/config.toml
```

After restarting your node, you should be able to access the tendermint metrics(default port is 26660): <http://localhost:26660>

### Configure Prometheus Targets

Append a `job` under the `scrape_configs` of your prometheus.yml

```yaml
      - job_name: irishub
        static_configs:
        - targets: ['<Validator-IP>:26660']
          labels:
            instance: validator
        - targets: ['<Sentry-0-IP>:26660']
          labels:
            instance: sentry-0
        - targets: ['<Sentry-1-IP>:26660']
          labels:
            instance: sentry-1
```

Reload prometheus config

```bash
curl -X POST http://<PROMETHEUS-IP>:9090/-/reload
```

### Import Grafana Dashboard

Copy and paste the [Grafana Dashboard ID](https://grafana.com/grafana/dashboards/11036) `11036` OR content of [cosmos-dashboard.json](cosmos-dashboard.json), click on `Load` to complete importing.

![import](imgs/import.jpg)
