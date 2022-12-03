## Ingress-controler-daemonset

Ajout dans le controller-daemonset le support tcp-udp dans les arguments du container

```
- --tcp-services-configmap=$(POD_NAMESPACE)/tcp-services
- --udp-services-configmap=$(POD_NAMESPACE)/udp-services
```

## ingress-configMap

Creer un ConfigMap, dans le ns ou est ingress, ici network.

**Exemple mssql :**
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: tcp-services
  namespace: network
data:
  1433: "poc/mssql-service:1433"  
```
------------------

## ingress-controler-service

On doit ajouter le port dans le service du controler ingress nginx ici 30001 

**Exemple mssql :**
```
- name: proxied-tcp-1433
  port: 1433
  targetPort: 1433
  nodePort: 30001
  protocol: TCP
```	  
-----------------


## Doc
https://kubernetes.github.io/ingress-nginx/user-guide/exposing-tcp-udp-services/

