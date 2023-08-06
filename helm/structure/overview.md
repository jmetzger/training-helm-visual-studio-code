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
  * helm get notes  


### charts/

  * Hier werden die abhängigen charts runtergeladen und als .tgz


