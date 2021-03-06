###Installing Necessary Software

-----

In order to work on cartography files, some software prerequisites need to be installed. This document will assume users are running macOS.

- Install [Homebrew](http://brew.sh)
- Install [Node and NPM](https://nodejs.org/en/) in its most recent LTS release
- Install shp2json with the following line in your terminal.
    - ```sudo npm install -g shapefile ```
- Install d3 with the following line in your terminal.
    - ```sudo npm install -g d3```

- Install d3 geography tools with the following line in your terminal.
    - ```sudo npm install -g d3-geo-projection```
- Install geographics data abstraction library with the following line in your terminal.
    - ```brew install gdal```
- Install topojson parser with the following line in your terminal.
    - ```sudo npm install -g topojson```
- Install Newline-Delimited Json Tools
    - ```sudo npm install -g ndjson-cli```
- Acquire a [Census API Key](http://api.census.gov/data/key_signup.html)
   
    
    
All of this software will come in handy in converting shapefiles, large collections of precise polygons of geographic features encoded as binary data for use with GIS tools, to human-readable json files. The tools also facilitate the manipulation of shapefiles, allowing use to combine other data with the geographic vectors.

First, we need to [collect some resources](resources.md).
