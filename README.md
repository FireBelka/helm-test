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
