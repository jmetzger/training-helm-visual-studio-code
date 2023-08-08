# Publish on Github 

## Prep 

```
Create new public repo with README.md
Go to Settings -> Pages -> an enable for branch "main"
git clone the repo locally
```

## Locally pack, index and upload it.  

```
git clone https://github.com/jmetzger/chart-test.git
# guestbook must be present as folder with charts 
helm package guestbook
cp guestbook-0.1.0.tgz chart-test/
helm repo index chart-test/
git add .
git commit -m "initial release"
git push -u origin main
```

## Work with it 

```
helm repo add githubrepo https://jmetzger.github.io/chart-test/
helm repo search guestbook
helm search repo guestbook
helm repo list
helm pull githubrepo/guestbook
```

