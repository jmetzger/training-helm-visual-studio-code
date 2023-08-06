# Überblick 

## Komponenten von Helm-Charts

### Chart.yml 

### Chart.lock (wird automatisch generiert) 

### templates/

#### _helper.tpl 

  * Enthält snippet die mit include oder templates inkludiert werden können
  * Konvention der Snippets mit define ChartName.Eigenschaft z.B. botti.fullname 

#### NOTES.txt 

  * Wird ausgegeben, nachdem das Chart installiert wurde
    * oder:
   
```
# after installation
# helm install my-botti -n my-application --create-namespace botti
helm get -n my-application notes my-botti
```

### charts/

  * Hier werden die abhängigen charts runtergeladen und als .tgz


