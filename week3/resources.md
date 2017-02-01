###File Resouces to Download

-----

In order to make an interactive, website-friendly spatial data visualization, we need a few important resources.

- Vector-set representing pertinent geographic features, culled to remove as many features as possible for performance.
- Dataset to plot, matching the geographic features as closely as possible.
- Code to project and draw the geographic features and plot the data.

We will take each of these steps in turn.

####Sourcing shapefiles

There are many free resources for pulling down high quality shapefiles.

- [Natural Earth Data](http://www.naturalearthdata.com)
- [US Census Shapefiles](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html)
- [Spatial Reference](http://spatialreference.org)
- [Statsilk](http://www.statsilk.com/maps/download-free-shapefile-maps)
- [Global Administrative Areas](http://www.gadm.org)

This tutorial will use Natural Earth Data's 1:50m cultural map, showing internal country subdivisions without large lakes. You can access that [file directly here](http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/50m/cultural/ne_50m_admin_0_sovereignty.zip). This provides a nice base to start upon, but it is likely that a more specific and targeted set of shapefiles will be useful for individual projects.

The binary shapefile we downloaded can be previewed at [mapshaper](http://mapshaper.org), which is a fast way to see the data inside of a shapefile without needing to go through the lengthy geojson conversion process.

Drag in the `.shp` file to view the contents of the shapefile. You should see the UN-recognized countries rendered in black lines, with some scattered red lines indicating intersecting vectors.

Please move the entire downloaded `ne_50m_admin_0_sovereignty` file to your Desktop.

####Matching Plottable Dataset
Download [this comma-separated-value file](refugee.csv). It contains historical data sourced from the [UNHCR](www.unhcr.org) on Refugee countries-of-origin from 2006 to 2014, the most recent study available.

Please move the `refugee.csv` downloaded file inside of the `ne_50m_admin_0_sovereignty` directory of your Desktop.

####Code for Visualization
This code will come from D3's excellent geospatial code library. We will use code similar to this [example](http://bl.ocks.org/rveciana/a2a1c21ca1c71cd3ec116cc911e5fce9) by Mike Bostock, the author of D3.

With all of these three pieces in place, we can move onto running the [complex data conversions](conversion.md) necessary to combine and render this data.
