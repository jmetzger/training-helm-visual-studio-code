# Upgrade 



## Problems with upgrade 

  * in some circumstances --reset-values are set
  * in come circumstances --reuse-values are set

### Default strategy:

  * if you are NOT set any values during upgrade, helm implicitly uses --reuse-values strategy
  * if you ARE setting values during upgrade, helm implicitly uses --reset-values strategy

## Strategy can get enforce 

  * --reuse-strategy or --reuse-values  

## Best choice (SOLUTION) , if you want to have values from the new chart version 

```
helm get values example-loki > prev-values.yaml
# Values from old chart are merge with new chart, with merge of set on top 
helm upgrade example-loki -f prev-values.yaml --set grafana.enabled=true
```

## Reference: 

  * https://shipmight.com/blog/understanding-helm-upgrade-reset-reuse-values
