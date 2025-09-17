# CSV 


## csvkit

```
pip install csvkit
```

| Description | command example | 
|-------|-----|
| Stats for a column | csvstat results.csv --columns success |

## csvtool

```
pip3 install git+https://github.com/maroofi/csvtool.git
```

| Description | command example | 
|-------|-----|
| Print Header | csvtool -r results.csv |
| Find a string in particular column | csvtool results.csv -c 14 -s 'True'| 
