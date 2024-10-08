# Monitoring of Docker & Nginx Metrics with Logs Using Prometheus, Loki & Grafana

### Step 1: Create a Docker Network
```
docker network create monitoring
```
### Step 2: Create a Docker Container
```
docker compose up -d 
```

### Step 3: Browse Grafana
```
http://localhost:3000/
```
### Step 4: Browse Prometheus
```
http://localhost:9090/targets?search=
```
we see the all metrics ```Endpoint``` here. If Docker endpoint state ```Down```. We need to modify the ```daemon.json``` file for  the docker API metrics endpoint details  <a href="https://docs.docker.com/engine/daemon/prometheus/">here</a> The code is of metrics addr:
```
"metrics-addr": "127.0.0.1:9323"
```

### Step 5: Login the Grafana 
**The access is :** username ```admin``` & Password  ```admin``` <br>

### Step 6: Add Data sources
For Prometheus address 

```
http://prometheus:9090
```
For Loki address 
```
http://loki:3100
```
### Step 7: Now Create Dashboards

1. Docker Container Running (datasource[prometheus])
```
engine_daemon_container_states_containers{state="running"}
```
2. Nginx Total Requests (datasource[prometheus])
```
nginx_http_requests_total
```
3. Nginx logs (datasource[loki])
```
{job="nginx"} |= ``
```
4. CPU Usage by container (datasource[prometheus])
```
sum(rate(container_cpu_usage_seconds_total{instance=~".*",name=~".*",name=~".+"}[5m])) by (name) *100
```
<br>
If, We want to see all metrics in a dashboard import the dashboard with this ID ```14282``` for Cadvisor exporter.

# Demo

![Monitoring  of Docker & Nginx Metrics with Logs Using Prometheus, Loki & Grafana](/cv-app/images/dashboard.png)

Thankyou for reading 👍

### 📣 Follow & Show Your Support ⭐️

If you found this project helpful, please give it a star! ⭐️ It helps others discover the project and motivates us to continue improving it.

Stay updated with my latest projects and articles:

- **GitHub**: Follow me on [GitHub](https://github.com/bjnandi) to see my latest repositories and contributions.  
  [![Follow @bjnandi](https://img.shields.io/github/followers/bjnandi?label=Follow%20%40bjnandi&style=social)](https://github.com/bjnandi)

- **Medium**: Follow me on [Medium](https://medium.com/@bjnandi) to read my latest articles and insights.  
  ![Medium Badge](https://img.shields.io/badge/Medium-Follow%20Me%20on%20Medium-000?logo=medium&style=social)

<br>
Thank you for your support and interest in my work! <br>
<br>

— — — — — — — — — — — — Happy DevOps Journey 💻✨— — — — — — — — — — — —