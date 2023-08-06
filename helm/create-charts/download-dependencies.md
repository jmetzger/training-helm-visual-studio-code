# Download Dependencies 

## Voraussetzung: 

  * Dependencies sind in Chart.yml eingetragen 
  * Achtung: Version ist die Version des Charts nicht der App !!! 

## Das 1. Mal 

```
# 1. Alle Abhängigkeiten werden in Form von .tgz - Archiven heruntergeladen
     -> in das charts - Verzeichnis
# 2. Eine Chart.lock - datei wird erstellt. (hält den aktuellen Stand fest)
# helm dependancy update $CHART_PATH
# botti erklärt sich gleich unten im Walkthrough 
helm dependancy update botti 
```

## Das 2. Mal (wenn Chart.lock vorhanden, aber charts/ muss nicht da sein 

```
helm dependancy build botti 
```

## List all dependencies 

```
helm dependancy list botti
```


## Walkthrough 

```
cd
helm create botti
```

```
cd botti
# add dependency
nano Chart.yml
```

```
# at the end of the file add

# After that save and exit STRG + O + ENTER , STRG  + X
```

```
# Update to download depdendancies 
cd ..
helm dependency update botti 
cd botti/charts
ls -la
cd ../../
```

```
# Add repo to be able to do helm dependency build
rm -fR botti/charts
# Chart.lock needs to be there
ls -la botti/Chart.lock

# Add repo / needs to be there, otherwice 
helm repo add bitnami https://charts.bitnami.com/bitnami
helm dependency build botti
```
