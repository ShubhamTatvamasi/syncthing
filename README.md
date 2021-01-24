# syncthing

Install syncthing:
```bash
kubectl create deployment syncthing --image=syncthing
kubectl expose deployment syncthing --port=8384 --name=syncthing
```

Setup ingress:
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: syncthing
spec:
  tls:
    - hosts:
      - syncthing.k8s.shubhamtatvamasi.com
      secretName: letsencrypt
  rules:
    - host: syncthing.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: syncthing
            servicePort: 8384
EOF
```

Delete everything:
```bash
kubectl delete deploy/syncthing svc/syncthing ing/syncthing
```
