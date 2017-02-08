###Data-Wrangling

-----

Often, the hardest part of producing the joined, uniform, and clean files necessary for data visualization is the messy process of combining disparate datasets. In particular, joining geoJSON files with any kind of dataset is always a pain. The process documented below demonstrates some of the challenges you will likely encounter. Know though from the start, that the most important prerequisite for joining datasets is that *some property must be shared between the datasets*. And, those properties must be the *id* of each element in both datasets.

We have two files to combine.

- `il_2015_tract.json` holding population data per census tract
- `il-cea.json` containing physical outlines of the census tracts

The geoJSON file that currently holds our geographic vectors `il-cea.json` is exactly one line long. Of course, that one line is 5.4MB long! It would be nice if, for each `Feature` representing each census tract, we had a single line. This would allow us to better understand the contents of the file and iterate through it more easily.

A recent development in data manipulation tools, Newline-Delimmited JSON or ndJSON, does just that.

```
ndjson-split 'd.features'  < il-cea.json  > il-cea.ndjson 
```

The ndJSON file is exactly the same in content, but each feature now occupies its own line, making the file much more easily browsable.

A single `Feature` now looks like this.

```
{"type":"Feature","properties":{"STATEFP":"17","COUNTYFP":"001","TRACTCE":"000100","AFFGEOID":"1400000US17001000100","GEOID":"17001000100","NAME":"1","LSAD":"CT","ALAND":12937184,"AWATER":22042},"geometry":{"type":"Polygon","coordinates":[[[243.50073728444158,448.78509337831144],[243.52734048022484,447.9103440677444],[243.546409815945,447.2830784788588],[243.55607335375944,446.9691828150982],[243.57438802172084,446.35419266865665],[243.57473305566097,446.34361983851034],[243.601938826974,445.47522069289676],[243.6243643282802,444.7997503199384],[244.15012541709052,444.80914965528893],[244.19792101597073,444.8105857541964],[244.8327744494682,444.82901346514984],[245.42392624558366,444.85177606482216],[246.02087386249704,444.8699389065622],[246.01769346867653,445.0722979056976],[246.4520992993404,444.89144190705576],[249.36282200744378,445.0407898076868],[249.2696557909751,446.60347210540203],[249.21977172859306,446.8948049945269],[248.9703406026203,447.51716296046084],[249.37386762913314,447.53024730063464],[249.4651075901962,447.6335525968086],[249.4504531856717,448.4575921372722],[249.39694447631373,450.0454003745282],[248.97307444172125,450.00221483194036],[248.22713212793465,450.01931669033206],[245.88725936773483,449.9492507810886],[244.70603839330875,449.91160534544645],[243.48097820090263,449.85404013512516],[243.4858468721869,449.6390958989026],[243.49729693139287,448.99695542522954],[243.50073728444158,448.78509337831144]]]}}
...
```

Note towards the beginning, there are called-out properties for `STATEFP` and `COUNTYFP` or State and County FIPS Identifier, and `TRACTCE` for the Census Tract Encoding Identifier. Those three numbers, joined together in sequence, make up the `GEOID` property.

Similarly, in the head of the `il_2015_tract.json` population file, we have the same properties.

```
[["B01003_001E","state","county","tract"],
["4558","17","001","000100"],
...
```

This means that the datasets can be combined! We will use the `TRACTCE` property of `il-cea.ndjson` and the `tract` property of `il_2015_tract.json` to knit these files together.

Let's *elevate* the `TRACTCE` property of `il-cea.ndjson` to each element's id.

```
ndjson-map 'd.id = d.properties.TRACTCE, d' < il-cea.ndjson > il-cea-id.ndjson
```

Note, at the very end of this object, we have the id assigned.

```
{"type":"Feature","properties":{"STATEFP":"17","COUNTYFP":"001","TRACTCE":"000100","AFFGEOID":"1400000US17001000100","GEOID":"17001000100","NAME":"1","LSAD":"CT","ALAND":12937184,"AWATER":22042},"geometry":{"type":"Polygon","coordinates":[[[243.50073728444158,448.78509337831144],[243.52734048022484,447.9103440677444],[243.546409815945,447.2830784788588],[243.55607335375944,446.9691828150982],[243.57438802172084,446.35419266865665],[243.57473305566097,446.34361983851034],[243.601938826974,445.47522069289676],[243.6243643282802,444.7997503199384],[244.15012541709052,444.80914965528893],[244.19792101597073,444.8105857541964],[244.8327744494682,444.82901346514984],[245.42392624558366,444.85177606482216],[246.02087386249704,444.8699389065622],[246.01769346867653,445.0722979056976],[246.4520992993404,444.89144190705576],[249.36282200744378,445.0407898076868],[249.2696557909751,446.60347210540203],[249.21977172859306,446.8948049945269],[248.9703406026203,447.51716296046084],[249.37386762913314,447.53024730063464],[249.4651075901962,447.6335525968086],[249.4504531856717,448.4575921372722],[249.39694447631373,450.0454003745282],[248.97307444172125,450.00221483194036],[248.22713212793465,450.01931669033206],[245.88725936773483,449.9492507810886],[244.70603839330875,449.91160534544645],[243.48097820090263,449.85404013512516],[243.4858468721869,449.6390958989026],[243.49729693139287,448.99695542522954],[243.50073728444158,448.78509337831144]]]},"id":"000100"}
...
```

Now, we need to convert the simple array notation of `il_2015_tract.json` into proper json for matching purposes.

```
ndjson-cat il_2015_tract.json > il_2015_tract_flat.json
```

This line removes all line breaks in the file and flattens out hierarchies. Useful for making sure unintentional whitespace doesn't get in the way of the following steps. Look at the file, it's one line long!

Let's now resplit the file into newlines as we did with our geographic features previously.

```
ndjson-split 'd.slice(1)' < il_2015_tract_flat.json > il_2015_tract_expanded.ndjson
```

We now have an ndJSON file, let's do some simple manipulation to prepare this file for merging. This line will format the resulting ndJSON objects with ids and population properties.

```
ndjson-map '{id: d[3], Population: d[0]}' < il_2015_tract_expanded.ndjson > il_2015_tract_withID.ndjson
```

And we have our goal!

```
{"id":"000100","Population":"4558"}
{"id":"000201","Population":"1900"}
{"id":"000202","Population":"2666"}
{"id":"000400","Population":"3399"}
{"id":"000500","Population":"2415"}
{"id":"000600","Population":"3759"}
{"id":"000700","Population":"1243"}
{"id":"000800","Population":"2929"}
```

And finally, to merge.

```
ndjson-join 'd.id'  il-cea-id.ndjson  il_2015_tract_withID.ndjson > il_joined.ndjson
```

And we have our result! Note the matched `Population` property at the end of the object.

```
[{"type":"Feature","properties":{"STATEFP":"17","COUNTYFP":"001","TRACTCE":"000100","AFFGEOID":"1400000US17001000100","GEOID":"17001000100","NAME":"1","LSAD":"CT","ALAND":12937184,"AWATER":22042},"geometry":{"type":"Polygon","coordinates":[[[243.50073728444158,448.78509337831144],[243.52734048022484,447.9103440677444],[243.546409815945,447.2830784788588],[243.55607335375944,446.9691828150982],[243.57438802172084,446.35419266865665],[243.57473305566097,446.34361983851034],[243.601938826974,445.47522069289676],[243.6243643282802,444.7997503199384],[244.15012541709052,444.80914965528893],[244.19792101597073,444.8105857541964],[244.8327744494682,444.82901346514984],[245.42392624558366,444.85177606482216],[246.02087386249704,444.8699389065622],[246.01769346867653,445.0722979056976],[246.4520992993404,444.89144190705576],[249.36282200744378,445.0407898076868],[249.2696557909751,446.60347210540203],[249.21977172859306,446.8948049945269],[248.9703406026203,447.51716296046084],[249.37386762913314,447.53024730063464],[249.4651075901962,447.6335525968086],[249.4504531856717,448.4575921372722],[249.39694447631373,450.0454003745282],[248.97307444172125,450.00221483194036],[248.22713212793465,450.01931669033206],[245.88725936773483,449.9492507810886],[244.70603839330875,449.91160534544645],[243.48097820090263,449.85404013512516],[243.4858468721869,449.6390958989026],[243.49729693139287,448.99695542522954],[243.50073728444158,448.78509337831144]]]},"id":"000100"},{"id":"000100","Population":"4558"}]
...
```

