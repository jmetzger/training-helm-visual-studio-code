# Upgrade 

## Walkthrough 

### Step 1: Upgrade 

```
helm install my-mariadb bitnami/mariadb -f db/prod-values.yaml --set auth.database=db1
helm get values my-mariadb
# prod-values will be overwritten, because of using --set -> defaults to using switch --reset-values (in the background) 
# for upgrade of mariadb, you will need passwort 
export MARIADB_ROOT_PASSWORD=$(kubectl get secret --namespace "jochen" my-mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 -d)
helm upgrade my-mariadb bitnami/mariadb --set auth.database=db2 --set  auth.rootPassword=$MARIADB_ROOT_PASSWORD
helm get values my-mariadb
# if you want to reuse the values from last release -> set --reuse-values
helm upgrade my-mariadb bitnami/mariadb --reuse-values --set  auth.rootPassword=$MARIADB_ROOT_PASSWORD
helm get values my-mariadb
```

### Step 2: Rollback 

```
helm history my-mariadb
helm rollback my-mariadb 1
```

## Problems with upgrade 

  * in some circumstances --reset-values are set
  * in come circumstances --reuse-values are set

### Default strategy:

  * if you NOT set any values during upgrade, helm implicitly uses --reuse-values strategy
  * if you ARE setting values during upgrade, helm implicitly uses --reset-values strategy

## Strategy can get enforce 

  * --reuse-strategy or --reuse-values  

## Best choice (SOLUTION) , if you want to have values from the new chart version 

```
helm get values example-loki > prev-values.yaml
# Values from old chart are merge with new chart, with merge of set on top 
helm upgrade example-loki -f prev-values.yaml --set grafana.enabled=true
```

## Reference: 

  * https://shipmight.com/blog/understanding-helm-upgrade-reset-reuse-values
