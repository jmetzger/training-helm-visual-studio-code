# Walkthrough 

## Attention: please only use it in the 

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
```

