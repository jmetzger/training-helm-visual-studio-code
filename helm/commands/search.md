# Suche in den Repos und im Hub 

## Suche im hub 

```
helm search hub mariadb
# Zeige kompletten Zeilen an ohne abszuschneiden
helm search hub mariadb --max-col-width=0
```

## Suche im Repo 

```
# Suche nach allen Charts, die mariadb im Namen oder der Beschreibung tragen 
helm search repo mariadb

# Zeige alle Version von charts an, die mit bitnami/mariadb beginnen 
helm search repo bitnami/mariadb --versions
```
