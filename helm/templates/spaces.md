# Templating - spaces

## Explanation 

  * {{- -> trim on left side
  * -}} -> trim on right side 
  * trim tabs, whitespaces a.s.o. (see ref)

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

```
# "{{23 -}} < {{- 45}}"
```

```
helm template .. 
helm template --debug ..
```

## Reference:

  * https://pkg.go.dev/text/template#hdr-Text_and_spaces
