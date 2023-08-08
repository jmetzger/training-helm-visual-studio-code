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

  * Decide how many chars to remove
  * mug: "true"* remove newlines
    

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ .Values.favorite.drink | default "tea" | quote }}
  food: {{ .Values.favorite.food | upper | quote }}*
**{{- if eq .Values.favorite.drink "coffee" }}
  mug: "true"*
**{{- end }}
```

## Step 3: (Problem) That will produce food: "PIZZA"mug: "true" because it consumed newlines on both sides.

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ .Values.favorite.drink | default "tea" | quote }}
  food: {{ .Values.favorite.food | upper | quote }}
  {{- if eq .Values.favorite.drink "coffee" -}}
  mug: "true"
  {{- end -}}

```

## Step 4: Best solution 

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ .Values.favorite.drink | default "tea" | quote }}
  food: {{ .Values.favorite.food | upper | quote }}
  {{- if eq .Values.favorite.drink "coffee"}}
  {{ "mug:true" }}
  {{- end }}
```

## Reference

  * https://helm.sh/docs/chart_template_guide/control_structures/
