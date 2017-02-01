The final step is to inject our refugee data into the geographic features.

The `refugee.csv` dataset contains a parameter called "name," the first column name if you open the file in Excel or Numbers, as does the Natural Earth Data files we've been working on. A slight edit to our topojson command will allow us to unite the two files based on this shared parameter with the -e option to reference the external hpi.csv file and --id-property option to choose the parameter to match. We can also rename the parameters in the resulting topoJSON file with the target=source syntax.
