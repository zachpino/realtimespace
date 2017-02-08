###Finally, We're Making a Data Visualization!

-----

Population is kind of boring to visualize, given that census tracts are by design aimed at including around 4,000 citizens. Instead, let's make use of the `ALAND` property, the land area in meters, included in our shapefile.

```
ndjson-map 'd[0].properties = {density: Math.floor(d[1].Population / d[0].properties.ALAND * 2589975.2356)}, d[0]' < il_joined.ndjson > il-density.ndjson
```

Here, we are making a new property called `density` that is the result of simplifying (via `Math.floor` which rounds down) the population divided by the land area in meters. To better match American mental models when we look at the data, we can multiply our square meters by 1609.34^2, the number of square meters in a square mile -- and end up with a unit conversion coefficient of `2589975.2356`. After this bit of math, we have a data point for population density for each census tract.

Now, let's add some color.

```
ndjson-map -r d3 '(d.properties.fill = d3.scaleSequential(d3.interpolateViridis).domain([0, 4000])(d.properties.density), d)'  < il-density.ndjson  > il-color.ndjson
```

All of that, in one line of code! 

We are adding another property, `fill`, to each census tract. The fill color is coming from a mapping to a perceptual color scale called `Viridis`. There are [many other perceptual color scales](https://github.com/d3/d3-scale/blob/master/README.md#interpolateViridis) available in d3. These scales take a `domain`, a high and low number (here the range of expected densities from 0 people/square mile to 4000 people/square mile), and a value (here `density`). Each value is placed within the domain, and is assigned a color based on where it falls in the `domain`. Values that are close together end up with similar colors, and low values receive low intensity colors and vice-versa.

Let's see it!

```
geo2svg -n --stroke none -p 1 -w 960 -h 960 < il-color.ndjson > il-color.svg
```

![sequential](http://www.zachpino.com/d3/il-color-reg.svg)

And, we have a visualization!

For slightly better results when confronted with a polarized dataset (we have lots of very high densities, and lots of very low densities in Illinois), we can take the square root of each value.

```
ndjson-map -r d3 '(d.properties.fill = d3.scaleSequential(d3.interpolateViridis).domain([0, 64])(Math.sqrt(d.properties.density)), d)'  < il-density.ndjson  > il-color-sqrt.ndjson
```

Note that we also took the square root of 4000 (~64) in the `domain` definition. Follow that up with svg conversion.

```
geo2svg -n --stroke none -p 1 -w 960 -h 960 < il-color-sqrt.ndjson > il-color-sqrt.svg
```

![sqrt](http://www.zachpino.com/d3/il-color.svg)

After all that data manipulation, we have the visualization we were looking for.
