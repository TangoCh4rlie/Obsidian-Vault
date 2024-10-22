# Microk8s deployement
[Uninstall](https://www.deploymastery.com/2023/05/24/how-to-uninstall-microk8s-on-ubuntu-20-04/)

[SetUp All installation](https://pacroy.com/single-node-kubernetes-on-home-lab-using-microk8s-metallb-and-traefik-7bb1ea38fcc2)

Installation du loadbalencer Metallb
microk8s enable metallb
plage d'adresses IP 192.168.1.42-192.168.1.45





# Minikube
Un `deployment.yaml`
```yaml
apiVersion: apps/v1  
kind: Deployment  
metadata:  
  name: k8s-microproject-deployment  
  namespace: virtu  
spec:  
  selector:  
    matchLabels:  
      app: microproject  
  template:  
    metadata:  
      labels:  
        app: microproject  
    spec:  
      containers:  
        - name: microprojectcontainer  
          image: tang0ch4rlie/k8s-microproject
```

Un `service.yaml`
```yaml
apiVersion: v1  
kind: Service  
metadata:  
  name: k8s-microproject-service  
  namespace: virtu  
  labels:  
    app: microproject  
spec:  
  selector:  
    app: microproject  
  ports:  
    - port: 3000  
      targetPort: 3000  
      protocol: TCP  
  type: NodePort
```

Un `ingress.yaml`
```yaml
apiVersion: networking.k8s.io/v1  
kind: Ingress  
metadata:  
  name: k8s-microproject-ingress  
  namespace: virtu  
spec:  
  tls:  
    - secretName: tls-secret  
      hosts:  
        - '*.microproject.com'  
  rules:  
    - host: microproject.com  
      http:  
        paths:  
          - path: /  
            pathType: Prefix  
            backend:  
              service:  
                name: k8s-microproject-service  
                port:  
                  number: 3000
```

`minikube addons enable ingress`



