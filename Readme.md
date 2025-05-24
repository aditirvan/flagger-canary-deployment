## Install Prometheus Stack
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm upgrade --install prom-stack prometheus-community/kube-prometheus-stack \
  --namespace monitoring --create-namespace \
  --values helm-values/prometheus.yaml
```

## Install MetalLB (required if onpremises)
```
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.9/config/manifests/metallb-native.yaml
kubectl apply -f metallb.yaml
```

## Install NGINX Ingress (metrics enabled)
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx --create-namespace \
  --values helm-values/nginx-ingress.yaml
```

## Install Flagger
```
helm repo add flagger https://flagger.app
helm repo update
helm upgrade --install flagger flagger/flagger \
  --namespace flagger-system --create-namespace \
  --values helm-values/flagger.yaml
```


## Deploy Application (deployment, services, ingress, canary)
```
kubectl apply -f deployment.yaml
```