# Create our first helm chart 

## Step 1: Create namespace and structure of helm chart 

```
cd
kubectl create ns guestbook-app
```

```
helm create guestbook
# now we have in folder "guestbook" 
# charts/
# Chart.yml
# templates
# values.yaml 
```

## Reference:

  * https://kubernetes.io/docs/tutorials/stateless-application/guestbook/
