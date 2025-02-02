# Grafana--tracking-cpu-local

<!-- Uploading "Giomo9DbYAY8HMK.jpeg"... -->


 # 📊 Grafana CPU Monitoring on Local Machine

This guide explains how to monitor CPU usage using **Prometheus**, **Node Exporter**, and **Grafana**.

## 🚀 Setup Instructions

### 1️⃣ Install Prometheus & Node Exporter

#### Install Prometheus
```sh
wget https://github.com/prometheus/prometheus/releases/latest/download/prometheus-linux-amd64.tar.gz
tar -xvzf prometheus-linux-amd64.tar.gz
cd prometheus-*
```

#### Configure Prometheus
Edit `prometheus.yml` and add the following:
```yaml
scrape_configs:
  - job_name: "node_exporter"
    static_configs:
      - targets: ["localhost:9100"]
```

#### Start Prometheus
```sh
./prometheus --config.file=prometheus.yml
```

#### Install & Start Node Exporter
```sh
wget https://github.com/prometheus/node_exporter/releases/latest/download/node_exporter-linux-amd64.tar.gz
tar -xvzf node_exporter-linux-amd64.tar.gz
cd node_exporter-*
./node_exporter
```

### 2️⃣ Install & Start Grafana
```sh
sudo apt-get install -y grafana
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

### 3️⃣ Add Prometheus as a Data Source in Grafana
1. Open Grafana in your browser: `http://localhost:3000`
2. Login with default credentials: `admin/admin`
3. Navigate to **Configuration** → **Data Sources** → **Add data source**
4. Select **Prometheus**, and set the URL to:
   ```
   http://localhost:9090
   ```
5. Click **Save & Test**

### 4️⃣ Create a Dashboard in Grafana
1. Navigate to **Create** → **Dashboard**
2. Click **Add a new panel**
3. Use this PromQL query for CPU usage:
   ```promql
   rate(node_cpu_seconds_total{mode="user"}[1m]) * 100
   ```
4. Click **Apply**, then **Save** your dashboard.


### Check logs for errors:
```sh
journalctl -u grafana-server --no-pager | tail -20
```

---

Now you have a fully functional Grafana dashboard for monitoring CPU usage on your local machine! 🚀


