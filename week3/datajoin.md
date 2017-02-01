The final step is to inject our refugee data into the geographic features.

The `refugee.csv` dataset contains a parameter called "name," the first column name if you open the file in Excel or Numbers. Each feature in the Natural Earth Data file we have been using does as well (check in Sublime or `less`). 

A slight edit to our `geo2topo` command will allow us to unite the two files based on this shared parameter with the -e option to reference the external `refugee.csv` file and `--id-property` option to choose the parameter to match. We can also rename the parameters in the resulting topoJSON file with the `target=source` syntax.

```
geo2topo -e refugee.csv --id-property name --properties population=pop_est,gdp=gdp_md_est,+2014 sovereign.json -o refugeeplot.topo.json
```

