# Default (proper way) 

## Prepare 

```
helm create testenv 
cd testenv/templates 
rm -fR *.yaml 
```

```
nano testdefault.yaml 
```

```
drink: {{ .Values.favorite.drink | default (printf "%s-tea" (include "fullname" .)) }}
```
