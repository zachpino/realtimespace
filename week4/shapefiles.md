###Census Shapefiles

-----

As discussed previously, shapefiles are readily available binary datastores native to GIS tracking systems, containing vector data based on spherical coordinate systems. The US government produces high quality shapefiles at various resolutions as part of the decennial census process.

[This page](http://www2.census.gov/geo/tiger/) includes links to most of the vector datasets available. Clicking through `GENZ2015` and `shp/` will reveal the useful directories. The `GENZ2015` reveals the year (2015), language (EN), and source of the vectors: the `GAZETEER` program, which produces medium-fidelity geographical vectors perfect for thematic visualizations and not precise positioning system (served by the `TIGER` program).

This web directory contains encoded data in various resolutions and formats. The filenames are composed of the following variables, a common practice of data producers.

```cb_[YEAR]_[FIPS CODE]_[GEOGRAPHIC SCALE UNIT]_[RESOLUTION]```

The FIPS codes, abbreviated from the Federal Information Processing Standard, are the ANSI preferred method for identifying American geographic entitites. You can browse them [here](https://www.census.gov/geo/reference/ansi_statetables.html), though this guide will assume Illinois [17].

From your computer's terminal (importantly not your server, as the programs we are about to run are not installed on your AWS box), we can pull down the necessary file.
