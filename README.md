# Task
 - Deploy Nginx Application
 - Set up logging for nignx pods using exporter
 - Configure monitoring using Prometheus and Grafana.
 - Create custom alerts based on specific metrics like CPU usage, memory consumption, etc.

# Steps to Achieve
Deploy the nginx application
 - `kubectl apply -f app1.yaml`

Deploy the prometheus stack uisng helm
 - `helm repo add prometheus-community https://prometheus-community.github.io/helm-charts`
 - `helm repo update`
 - `helm install monitoring prometheus-community/kube-prometheus-stack`

Deploy the nginx exporter to get ngixn application metrics and post it to prometheus
 - `helm install nginx-exporter prometheus-community/prometheus-nginx-exporter -f values.yaml`

**Once the nginx exporter is deployed, it will connect to nginx service and get the nginx metric.**

**prometheus-nginx-exporter uses serviceMonitor to add the target into prometheus pod without changing any prometheus file**

Verify if everything is working as expected:
 - Access the grafana ui and login into it
 - `kubectl port-forward svc/monitoringrafana 3000:80`

- import the dashboard manually using the file `nginx_status_dashboard.json` and verify the nginx metrics.