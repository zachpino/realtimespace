In order to work on cartography files, some software prerequisites need to be installed. This document will assume users are running macOS.

- Install [Homebrew](http://brew.sh)
- Install [Node and NPM](https://nodejs.org/en/) in its most recent LTS release
- Install shp2json with the following line in your terminal.
```sudo npm install -g shapefile ```
- Install d3 geography tools with the following line in your terminal.
```sudo npm install -g d3-geo-projection```
- Install geographics data abstraction library with the following line in your terminal..
```brew install gdal```
- Install topojson parser with the following line in your terminal..
    - ```npm install -g topojson```
    
All of this software will come in handy in converting shapefiles, large collections of precise polygons of geographic features encoded as binary data for use with GIS tools, to human-readable json files. The tools also facilitate the manipulation of shapefiles, allowing use to combine other data with the geographic vectors.
