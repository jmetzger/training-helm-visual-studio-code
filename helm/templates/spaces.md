# Templating - spaces

## Walkthrough 

```
# When ever we encounter error while parsing yaml, we can use comment !!!
helm create testenv
cd testenv/templates
rm -f *.yaml
```

```
nano test.yaml
```

  * Explanation: 
    * {{- -> trim on left side
    * -}} -> trim on right side 



```
# "{{23 -}} < {{- 45}}"
```

```
helm template .. 
helm template --debug ..
```


## Reference:

  * https://pkg.go.dev/text/template#hdr-Text_and_spaces
