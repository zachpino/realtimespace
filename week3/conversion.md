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

`less` previews a small chunk of the output file.

We could have used `ogr2ogr`, a component of the GDAL library, to cut down on the contents of our features.

```ogr2ogr -f GeoJSON -where "subregion IN ('South Asia')" southasia.json ne_110m_admin_0_sovereignty.shp```


