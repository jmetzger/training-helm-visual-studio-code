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
# Chart.yaml
# templates
# values.yaml 
```

## Step 2: Explore templates folder and cleanup 

```
cd templates
ls -la
rm -fR tests
```

## Step 3: Explore the Chart.yaml 

```
cd ..
cat Chart.yaml
```

```
# type: Application or Library # please explain !
# dependencies - what other charts are needed - we will download them by helm command and they will be put in the charts - folder
```

## Step 4: Add redis as dependency 

```
# find the redis chart 
helm search hub --max-col-width=0  redis | grep bitnami
# adding the repo for bitnami
helm repo add bitnami https://charts.bitnami.com/bitnami
```

```
# now find the availabe versions (these are the chart versions
helm search repo redis --versions
```

```
nano Chart.yaml
```

```
# now add the dependency-block at the end of the file
dependencies:
  - name: redis
    version: "17.14.x"  # quotes are important here
    repository: https://charts.bitnamicom/bitnami
```

```
# Save the file and leave nano:
STRG + o + RETURN -> then -> STRG + x
```

```
cd ..
helm dependency update guestbook
```

```
# explore the newly populated folder
cd guestbook/charts
ls -la
cd ../..
```

## Modifying the values.yaml file 

```
# the version might have changed since i wrote this / adjust
helm show values charts/redis-17.14.5.tgz
helm show values charts/redis-17.14.5.tgz | grep -B 4 -i fullnameoverride
```

## Reference:

  * https://kubernetes.io/docs/tutorials/stateless-application/guestbook/
