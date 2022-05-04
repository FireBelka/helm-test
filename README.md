# nginx-ingress with ssl sertification(letsencrypt)
1) install nginx-controller (https://kubernetes.github.io/ingress-nginx/deploy/#azure):   
kubectl apply -f ingress-install.yaml (kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/cloud/deploy.yaml)
2) attach DNS label to ingress public IP
3) create backend pool
4) http ingress rule:   
kubectl apply -f ingress-rule-start.yaml
5) install cert-manager:    
kubectl apply -f cert-manager.yaml (kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.8.0/cert-manager.yaml)
6) install cluster-issuer:   
kubectl apply -f staging_issuer.yaml
7) https ingress rule:    
kubectl apply -f ingress-rule-ssl.yaml
8) kubectl describe certificate

# Prometheus
## Install
[helm chart prometheus-operator](https://github.com/prometheus-community/helm-charts.git)
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
kubectl create ns monitoring
helm show values chart/name > prometheus-values.yaml
```
edit values (prometheus-values.yaml)
```
helm install my-prometheus prometheus-community/kube-prometheus-stack -n monitoring -f prometheus-values.yaml
```
defaul grafana pass prom-operator
## Custom metrics
1) App in default namespace with metrics on /metrics (demo-custom-metrics folder)
2) edit values (prometheus-values.yaml; additionalScrapeConfigs section)
3) helm upgrade my-prometheus prometheus-community/kube-prometheus-stack -n monitoring -f prometheus-values.yaml
