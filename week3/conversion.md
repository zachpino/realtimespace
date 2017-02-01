###Converting Files

-----

The downloaded shapefile is a *binary* file, it does not permit easy human reading and editing. This makes it challenging to match our dataset to geographic features, since we are not able to see how any of the entities are named. Our first step will be to convert this file into something more usable.

Open a terminal, and move to the folder we prepared on your Desktop. ```cd ~/Desktop/ne_50m_admin_0_sovereignty/```

It is easy to convert the shapefile into a human readable format.

```shp2json ne_50m_admin_0_sovereignty.shp -o sovereign.json```

The `-o` option allows us to specify the location and name of the output file. The -n option places each *feature*, a geographical entity, on a new line.

After a short delay, the Terminal will return a prompt. 

You can view the complex results with the following line in your Terminal.

```less sovereign.json```

`less` previews a small chunk of the output file. Note the different parameters that each feature contains, for instance `subregion` geopolitical sub-region and `pop_est` estimated population.

We could have used `ogr2ogr`, a component of the GDAL library, to cut down on the contents of our features and convert as well, though `shp2json` is more efficient.

```ogr2ogr -f GeoJSON -where "subregion IN ('Central Asia')" centralasia.json ne_50m_admin_0_sovereignty.shp```

It is a weird Bash command, which specifies an output file *before* its input file.

This limits our map to only include features tagged with a `subregion` of `Central Asia`.

The final step in converting files is to take our geoJSON file, a very precise file format used mostly in GPS applications, and convert a less precise file for web usage.

```topojson -o sovereign.topo.json sovereign.json```




