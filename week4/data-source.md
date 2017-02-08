### Sourcing Data
-----

With a census API key, we can pull down data to embed in our census tract vectors. This example will use census tract population.

The [Census API documentation](http://www.census.gov/data/developers/data-sets/acs-5year.html), like most APIs, is challenging at first glance. Always look first at any examples provided. The page gives this example call for a structured request of the census datastore.

```
api.census.gov/data/2015/acs5?get=NAME,B01001_001E&for=state:*&key=...
```

`api.census.gov/data/` is the container for the US governments published data.

`2015/` is the year this data was published, nicely matching our shapefiles! The churn of politics results in constantly shifting geographic boundary lines. Try to always match the temporal stamp of your shapefiles and datasets as closely as possible.

`acs5/` is the name of this particular dataset: the American Community Survey 5-Year Data project.

The `get=...` section of this request identifies what data we are seeking. The `NAME` or the long alphanumeric string `B01001_001E` are pulled from this linked [variable reference](http://api.census.gov/data/2015/acs5/variables.html). Different encoded character strings access different parameters of the data. We will use straightforward population data, encoded at `B01003_001E`.

`for=state:*` says that we are interested in data scoped to the state level, and that we want all (the * wildcard) of the states.

`&key=...` is indicating that we will need 

More examples are [here](http://api.census.gov/data/2015/acs5/examples.html). Try to disentangle them for practice!

We can access the data that we want as follows.

```
curl 'http://api.census.gov/data/2015/acs5?get=B01003_001E&for=tract:*&in=state:17&key=[YOUR PERSONAL CENSUS KEY]' -o il_2015_tract.json
```

The additional `in:state:17` logic was pulled from one of the additional examples linked above. Again, note the FIPS code for Illinois.

We now have a dataset that looks like this, pulled from the census API.

```
[["B01003_001E","state","county","tract"],
["4558","17","001","000100"],
["1900","17","001","000201"],
["2666","17","001","000202"],
["3399","17","001","000400"],
["2415","17","001","000500"],
["3759","17","001","000600"],
["1243","17","001","000700"],
["2929","17","001","000800"],
["2603","17","001","000900"],
["3737","17","001","001001"],
["3645","17","001","001002"],
["8076","17","001","001100"],
["4333","17","001","010100"],
["3524","17","001","010200"],
["6083","17","001","010300"],
["3219","17","001","010400"],
["3040","17","001","010500"],
["5952","17","001","010600"],
["2392","17","003","957600"],
["1893","17","003","957700"],
["1733","17","003","957800"],
["1346","17","003","957900"],
["2868","17","005","951200"],
["6790","17","005","951300"],
["3179","17","005","951400"],
["4476","17","005","951500"],
...
```

We have, in columns from left to right...
 
- 2015 Population
- FIPS State Code
- FIPS Internal-to-Illinois County Code
- Tract Identifier

Now, we can merge this data with our shapefiles to produce our visualization.
