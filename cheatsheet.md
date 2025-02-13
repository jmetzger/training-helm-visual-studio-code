# Most important commands 

## Add repo for usage 

```
helm repo add bitnami <url-of-repo>
```


##  -A show all releases across all namespaces 

```
helm list -A
```

## Download chart an untar it (create a folder instead of archive) 

```
# Downloads it and creates folder mariadb in current directory 
helm pull bitnami/mariadb --untar 
```
