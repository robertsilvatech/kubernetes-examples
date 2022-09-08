# Ingress controller

Referência: 
- https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/

- Clonar o repositório e acessar a pasta de deployments

```shell
$ git clone https://github.com/nginxinc/kubernetes-ingress.git --branch v2.3.0
$ cd kubernetes-ingress/deployments
```

kubectl apply -f common/crds/k8s.nginx.org_virtualservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_virtualserverroutes.yaml
kubectl apply -f common/crds/k8s.nginx.org_transportservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_policies.yaml
