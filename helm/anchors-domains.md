# Walkthrough 

## Attention: please only use it in the values - file 

```
helm create training
```

## Example with Domains

```
variables:
  - &globalDomain "app.mydomain.de"
subchart1:
   domain: *globalDomain 
ingress:
   host: *globalDomain
```

```
helm install training training -f anchor-values.yaml
helm get values  
```

## Reference:

  * https://helm.sh/docs/chart_template_guide/yaml_techniques/#yaml-anchors
