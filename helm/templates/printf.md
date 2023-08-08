# printf example (with 2 arguments) 

```
# drink: {{ .Values.favorite.drink | default (printf "%s-tea-%s" (include "testenv.fullname" .) "foo") }}
```
