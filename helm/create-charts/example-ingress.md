# Beispiel Ingress 

```
cd
helm create testprojekt
cd testprojekt
cd templates
```

```
mkdir routes/
cd routes
nano 01-redirect.yaml
```

## Schritt 1: Mit der Basis anfangen

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    nginx.ingress.kubernetes.io/permanent-redirect: https://www.google.de
    nginx.ingress.kubernetes.io/permanent-redirect-code: "308"
  creationTimestamp: null
  name: destination-home
  namespace: my-namespace
spec:
  rules:
  - host: web.training.local
    http:
      paths:
      - backend:
          service:
            name: http-svc
            port:
              number: 80
        path: /source
        pathType: ImplementationSpecific
```

## Schritt 2: values - file mit eigenen Werten ergänzen (Default - Werte) 

```
# cd ../..
# nano values.yaml
# Zeilen ergänzt.
# Achtung: Eigenschaft UNBEDINGT ! ohne "-" 
myRedirect:
  url: "http://www.google.de"
  code: 302
```

## Schritt 3: Variablen aus values in template einbauen 

```
cd templates/routes
```

```
# nano 01-redirect.yaml 
# Neue Fassung: Alle Änderungen beginnen mit Platzhalter - Zeichen {{

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    nginx.ingress.kubernetes.io/permanent-redirect: {{ .Values.myRedirect.url }}
    nginx.ingress.kubernetes.io/permanent-redirect-code: {{ .Values.myRedirect.code | quote }}
  creationTimestamp: null
  name: destination-home
  namespace: my-namespace
spec:
  rules:
  - host: web.training.local
    http:
      paths:
      - backend:
          service:
            name: http-svc
            port:
              number: 80
        path: /source
        pathType: ImplementationSpecific
```

## Schritt 4: Test mit Default - Werten aus values.yaml 

```
helm template ../..
# achten auf ausgaben von Ingress
helm template ../.. | grep -A 40 "kind: Ingress" 
```

## Schritt 5: Default - Werte überschreibung für Produktion mit speziellen prod-values.yaml (Name beliebig) 

```
# Empfehlung: ausserhalb des Charts anlegen
cd
nano prod-values.yaml
```

```
myRedirect:
  url: "http://www.stiftung-warentest.de"
```

```
# Testen wie folgt
helm template -f prod-values.yaml testprojekt
# oder aber auch testen mit validate
helm template --validate -f prod-values.yaml testprojekt
# oder aber direkt release installation
helm install --dry-run -f prod-values.yaml testprojekt
```
