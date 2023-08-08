# With 

## Walkthrough 

### Preparation 

```
helm create testenv
cd testenv/templates
rm -fR *.yaml
```

```
# vi values.yml
# Adjust values.yaml file accordingly
favorite:
  food: PIZZA
  drink: coffee
```

### Step 1: 

```
# nano cm.yaml
```

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  {{- with .Values.favorite }}
  drink: {{ .drink | default "tea" | quote }}
  food: {{ .food | upper | quote }}
  {{- end }}
```

### Step 2a: Does not work because scope does not fit 

```
  {{- with .Values.favorite }}
  drink: {{ .drink | default "tea" | quote }}
  food: {{ .food | upper | quote }}
  release: {{ .Release.Name }}
  {{- end }}

```

### Step 2b: Solution 1: (Outside with) 

```
  {{- with .Values.favorite }}
  drink: {{ .drink | default "tea" | quote }}
  food: {{ .food | upper | quote }}
  {{- end }}
  release: {{ .Release.Name }}

```

### Step 2c: Changing the scope 

```
  {{- with .Values.favorite }}
  drink: {{ .drink | default "tea" | quote }}
  food: {{ .food | upper | quote }}
  release: {{ $.Release.Name }}
  {{- end }}

```

