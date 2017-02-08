###Shapefile Conversion
-----

Now, with shapefile vectors in hand from the Census, we can begin the task of producing our visualization. Let's first make the file easier to understand by making it human-readable.

```
shp2json cb_2015_17_tract_500k.shp -o il.json
```

Now we have a file we can make sense of!

```
{"type":"FeatureCollection","bbox":[-91.51307899999999,36.970298,-87.494756,42.508480999999996],"features":[{"type":"Feature","properties":{"STATEFP":"17","COUNTYFP":"001","TRACTCE":"000100","AFFGEOID":"1400000US17001000100","GEOID":"17001000100","NAME":"1","LSAD":"CT","ALAND":12937184,"AWATER":22042},"geometry":{"type":"Polygon","coordinates":[[[-91.377662,39.941598],[-91.377595,39.946645],[-91.37754699999999,39.950264],[-91.377522,39.952075],[-91.377478,39.955622999999996],[-91.377477,39.955684],[-91.377404,39.960694],[-91.377337,39.964591],[-91.373092,39.964605999999996],[-91.372706,39.964604],[-91.36757899999999,39.964580999999995],[-91.362804,39.964527],[-91.35798299999999,39.9645],[-91.357975,39.963333],[-91.35449899999999,39.964431999999995],[-91.33098199999999,39.963944999999995],[-91.331479,39.954924],[-91.331834,39.953238],[-91.333745,39.949618],[-91.33048699999999,39.949594],[-91.329734,39.94901],[-91.329718,39.944257],[-91.32989099999999,39.935095],[-91.333317,39.935289999999995],[-91.339331,39.935096],[-91.358216,39.935198],[-91.36775,39.935261],[-91.377641,39.935432],[-91.37763799999999,39.936672],[-91.37765399999999,39.940376],[-91.377662,39.941598]]]}},{"type":"Feature","properties":{"STATEFP":"17","COUNTYFP":"007","TRACTCE":"010300","AFFGEOID":"1400000US17007010300","GEOID":"17007010300","NAME":"103","LSAD":"CT","ALAND":3938550,"AWATER":864},"geometry":{"type":"Polygon","coordinates":[[[-88.861344,42.247111],[-88.861254,42.251289],[-88.86125799999999,42.251563],[-88.861267,42.253375999999996],[-88.852983,42.253189],[-88.846535,42.254251],[-88.840469,42.256575],[-88.84166499999999,42.255764],[-88.84164,42.253627],[-88.839078,42.253631999999996],[-88.839114,42.24776],[-88.839147,42.240893],[-88.84091,42.240871999999996],[-88.841669,42.240863],[-88.84174999999999,42.233683],[-88.86123099999999,42.233539],[-88.86144499999999,42.240472],[-88.861344,42.247111]]]}},{"type":"Feature","properties":{"STATEFP":"17","COUNTYFP":"019","TRACTCE":"000200","AFFGEOID":"1400000US17019000200","GEOID":"17019000200","NAME":"2","LSAD":"CT","ALAND":1415371,"AWATER":0},"geometry":{"type":"Polygon","coordinates":[[[-88.238337,40.121649999999995],[-88.237462,40.123756],[-88.236001,40.12726],[-88.234473,40.130932],[-88.232787,40.134997],[-88.231995,40.135005],[-88.23112599999999,40.135014],[-88.230308,40.135022],[-88.22911099999999,40.135033],[-88.229081,40.132436999999996],[-88.229248,40.131924999999995],[-88.229248,40.131031],[-88.229248,40.129407],[-88.22795099999999,40.128965],[-88.225639,40.128671],[-88.225966,40.127342],[-88.228883,40.127320999999995],[-88.22887999999999,40.126098999999996],[-88.22887999999999,40.125918999999996],[-88.228112,40.125903],[-88.228112,40.124703],[-88.228928,40.124703],[-88.228928,40.124545],[-88.228926,40.122167],[-88.228926,40.120252],[-88.228814,40.117366],[-88.229013,40.116369],[-88.230431,40.116364],[-88.23210499999999,40.116357],[-88.235419,40.116341999999996],[-88.24051999999999,40.116318],[-88.238337,40.121649999999995]]]}},{"type":"Feature","properties":{"STATEFP":"17","COUNTYFP":"019","TRACTCE":"000700","AFFGEOID":"1400000US17019000700","GEOID":"17019000700","NAME":"7","LSAD":"CT","ALAND":2574576,"AWATER":65},"geometry":{"type":"Polygon","coordinates":[[[-88.25797299999999,40.135073],[-88.254145,40.134809],[-88.238908,40.134924],[-88.233165,40.134992],[-88.232787,40.134997]...
```

Each `Feature` in the flie defines a census tract, and is tagged with `properties` such as State, County, Tract, and Geographic IDs as well as some broad notation on land and water area and the critical vector coordinates.

We can now manipulate this file with some simple projection math so that Illinois is easier to see! 

```
geoproject 'd3.geoConicEqualArea().rotate([90,-35]).fitSize([960,960],d)' < il.json > il-cea.json'
```

There are several new things in this line. This is the first line of Javascript we've covered. The `geoproject` command takes as input a javascript phrase, accessing the [d3 projection library](https://github.com/d3/d3-geo/blob/master/README.md#projections) directly.  Here, we are tapping the Conic-Equal-Area projection which does not distort the area of enclosed geography. This makes it ideal for visualizations where areas are meaningful, like chloropleths. Alternatives would be fine here, and consulting the [State Plane](https://github.com/veltman/d3-stateplane) guidelines, the preferred projection by each state government, is also advisable.

Projections have `rotate` methods that allow us to spin the globe and focus on a center point. Here, we are rotating the globe 90 degrees west away from the Prime Meridian, and 35 degrees towards the north pole to bring Illinois roughly into focus. You can see these numbers are meaningful -- Chicago's Longitude, Latitude coordinates are [41.8781° N, 87.6298° W]

Finally, we are scaling our projection to fit in a 960 point square. 

`geoproject` takes an input file with the `<` operator, and outputs a new file with the redirect `>` operator.

Let's get some usable vectors for design purposes!

```
geo2svg -w 960 -h 960 < il-cea.json > il-cea.svg
```

Let's now make this visualization [present some data](data-source)!
