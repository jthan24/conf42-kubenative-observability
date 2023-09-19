
# Create a cluster on AWS

> Please skip if you already have a kubernetes cluster

```bash
# I just added time to check the taken time for creation process
# Normally this process taken 15 minutes
time eksctl create cluster --version=1.27 --name=conf42-kubenative
```

## Using an alias for kubectl
```
alias k=kubectl
```

# Install an opentelemrtry demo
```bash
# Option 1 using HELM package manager
helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts
helm repo update open-telemetry
helm install my-otel-demo open-telemetry/opentelemetry-demo
helm install my-otel-demo open-telemetry/opentelemetry-demo --version=0.21.1

# Option 2 using kubectl directly
kubectl create namespace otel-demo
kubectl apply --namespace otel-demo -f https://raw.githubusercontent.com/open-telemetry/opentelemetry-demo/main/kubernetes/opentelemetry-demo.yaml
```

## Access to deployed stack
```bash
kubectl port-forward svc/my-otel-demo-frontendproxy 8080:8080
```
### References pages
Web store: http://localhost:8080/
Grafana: http://localhost:8080/grafana/
Jaeger UI: http://localhost:8080/jaeger/ui/


# Cleanup 
```bash
eksctl delete cluster conf42-kubenative
```

# References:
https://eksctl.io/introduction/
https://opentelemetry.io/docs/demo/kubernetes-deployment/
