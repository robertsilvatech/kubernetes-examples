# NetworkPolicy

<namespace>.svc.cluster.local
svc.cluster.local


- Criar os namespace

```bash
kubectl apply -f namespace.yaml 
```

- Criar os pods busybox em cada namespace (apenas para usar os utilitários no linux)

```bash
kubectl apply -f busybox.yaml -n blue-ns
kubectl apply -f busybox.yaml -n red-ns 
```

- Criar deployment e services **blue** e **red**
   
```bash
kubectl apply -f deployment-blue.yaml
kubectl apply -f deployment-red.yaml
kubectl apply -f service.yaml
```

- Testar comunicação

```bash
kubectl -n red-ns exec busybox -- wget -S http://blue.blue-ns.svc.cluster.local:5000
```
Output
```bash
Connecting to blue.blue-ns.svc.cluster.local:5000 (10.245.222.48:5000)
  HTTP/1.1 200 OK
  Server: Werkzeug/2.2.2 Python/3.9.13
  Date: Fri, 09 Sep 2022 00:19:24 GMT
  Content-Type: text/html; charset=utf-8
  Content-Length: 408
  Connection: close
  
saving to 'index.html'
index.html           100% |********************************|   408  0:00:00 ETA
'index.html' saved
```

- Aplicar network policy

```bash
kubectl apply -f networkpolicy.yam
```

- Validar conexão novamente

```bash
kubectl -n red-ns exec busybox -- wget -S http://blue.blue-ns.svc.cluster.local:5000
```

Output
```bash
Connecting to blue.blue-ns.svc.cluster.local:5000 (10.245.222.48:5000)
wget: can't connect to remote host (10.245.222.48): Connection timed out
command terminated with exit code 1
```