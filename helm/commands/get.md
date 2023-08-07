# Get information from release 

```
# Zeige alle user geänderten values an 
helm get values my-mariadb
# Zeige alle values, auch defaults an 
helm get values my-mariadb --all
# Zeige angewendete manifests an 
helm get manifest my-mariadb
# Zeige die hooks an, wenn vorhanden
helm get hooks my-mariadb 
# Zeige nochmals die Notes an
helm  get notes my-mariadb


```
