# Walkthrough 

## Attention: please only use it in the values - file 

```
helm create training
```

```
# Side by side to the training folder create a
# anchor-values.yaml
coffee: "yes, please"
favorite: &favoriteCoffee "Cappuccino"
coffees:
  - Latte
  - *favoriteCoffee
  - Espresso
```

```
helm install training training -f anchor-values.yaml
helm get values  
```

## Example with Elements 

```
coffee: "yes, please"
variables:
  - &FavoriteCoffee "Cappuccino"
  - &AnotherCoffee "Mokka"
coffees:
  - Latte
  - *FavoriteCoffee
  - Espresso
  - *AnotherCoffee
```

## Reference:

  * https://helm.sh/docs/chart_template_guide/yaml_techniques/#yaml-anchors
