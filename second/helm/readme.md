# Helm charts

## Traefik

Traefik installed with:
```
helm upgrade --install -n traefik traefik traefik/traefik -f .\traefik.yml
```

## ArangoDB 

Installed with
```
helm upgrade --install -n database -f .\arangodb.yml arangodb-operator .\charts\kube-arangodb-1.2.34.tgz
```
