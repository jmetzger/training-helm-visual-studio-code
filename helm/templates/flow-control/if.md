# If 

## Prepare (if not done yet)

```
helm create testenv
cd testenv/templates
rm -f *.yaml
```

## Step 1: Simple inline

```
nano iftest.yaml
```

```
# Adjust values.yaml file accordingly
favorite:
  food: PIZZA
  drink: coffee
```

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ .Values.favorite.drink | default "tea" | quote }}
  food: {{ .Values.favorite.food | upper | quote }}
  {{ if eq .Values.favorite.drink "coffee" }}mug: "true"{{ end }}

```

```
helm template ..
```


## Step 2: 


## Step 3:

## Reference

  * https://helm.sh/docs/chart_template_guide/control_structures/
