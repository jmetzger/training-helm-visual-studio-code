# Installation kubectl unter Linux 

## Walkthrough (Start with unprivileged user like training or kurs)

```
sudo su -
```

```
# Get current version
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
# install the kubectl to the right directory
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
