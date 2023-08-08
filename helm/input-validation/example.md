# Input Validierung 

## Walkthrough 

```
cd
helm create inputtest
cd inputtest
cd templates/
rm d* h* i* servicea*
rm -fR tests
```

```
# nano service.yaml mit folgendem Inhalt
apiVersion: v1
kind: Service
metadata:
  name: {{ include "inputtest.fullname" . }}
  labels:
    {{- include "inputtest.labels" . | nindent 4 }}
spec:
{{- $serviceType := list "ClusterIP" "NodePort" }}
{{- if has .Values.service.type $serviceType }}
  type: {{ .Values.service.type }}
{{- else }}
  {{- fail "value 'service.type' must be either 'ClusterIP' or 'NodePort'" }}
{{- end }}
{{- end }}
  ports:
    - port: {{ .Values.service.port }}
      targetPort: http
      protocol: TCP
      name: http
  selector:
    {{- include "inputtest.selectorLabels" . | nindent 4 }}

```
