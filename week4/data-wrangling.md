###Data-Wrangling

-----

Often, the hardest part of producing the joined, uniform, and clean files necessary for data visualization is the messy process of combining disparate datasets. In particular, joining geoJSON files with any kind of dataset is always a pain. The process documented below demonstrates some of the challenges you will likely encounter. Know though from the start, that the most important prerequisite for joining datasets is that *some property must be shared between the datasets*.

The geoJSON file that currently holds our geographic vectors `il-cea.json` is exactly one line long. Of course, that one line is 5.4MB long! It would be nice if, for each `Feature` representing each census tract, we had a single line. This would allow us to better understand the contents of the file and iterate through it more easily.

A recent development in data manipulation tools, Newline-Delimmited JSON or ndJSON, does just that.

```
ndjson-split 'd.features'  < il-cea.json  > il-cea.ndjson 
```

The ndJSON file is exactly the same in content, but each feature now occupies its own line, making the file much more easily browsable.





