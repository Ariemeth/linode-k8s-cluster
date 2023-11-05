# Cluster setup

## Setup namespaces

```
kubectl -n gearforce apply -f 00-namespaces.yml
```

## Install Traefik

```
helm upgrade --install -n traefik traefik traefik/traefik -f .\traefik.yml
```

## Install ArangoDB
```
helm upgrade --install  -n database -f .\arangodb.yml arangodb-operator .\charts\kube-arangodb-1.2.34.tgz
```

## Install ArangoDB cluster
```
kubectl -n database apply -f .\02-arangodb-cluster.yml
```

## Install Game Storage
Install from the gearforce_storage repo
```
helm upgrade --install -n storage --set replicaCount=2  --set database.address=${{ secrets.DB_ADDRESS }} --set database.user=${{ secrets.DB_USER }} --set database.password=${{ secrets.DB_PASS }} gs1 chart/gamestorage
```

## Install gearforce

```
helm upgrade --install -n gearforce gf1  .\chart\gearforce\
```

## Setup ingress

```
kubectl -n gearforce apply -f 04-redirect-scheme.yml -f 06-gs-ingressRoute.yml -f 06-gf2-ingressRoute.yml
```