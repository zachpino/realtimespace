###Geography

---

We have a map of cities, but no geography. This code is a bit advanced, walk through it one block at a time.

```
<!DOCTYPE html>
<html>
<head>
	<title>Realtime Weather Map</title>
	<meta http-equiv="cache-control" content="max-age=0" />
	<meta http-equiv="cache-control" content="no-cache" />
	<meta http-equiv="expires" content="0" />
	<meta http-equiv="expires" content="Tue, 01 Jan 1980 1:00:00 GMT" />
	<meta http-equiv="pragma" content="no-cache" />
	<style>
		path{
			stroke:#bdb;
			fill:#acb;
		}
	</style>
</head>
<body>
	<script src="https://d3js.org/d3.v4.min.js"></script>

	<script>

		var width = 1400;
		var height = 700;
		var cities = "4887398,361058,108410,6542286,146268,993800,4140963,256637,3941584,5391959,1857910,1642911,2624652,6547294,1819730,4553433,344979,3652462,1512569,1850147";
		var apikey = "2166f8d720eac7933e445a19f97cf00a";


		// set the domain and ranges for latitude and longitude
		var x = d3.scaleLinear().domain([-180,180]).range([0, width]);
		var y = d3.scaleLinear().domain([-90,90]).range([height, 0]);
		var tmp = d3.scaleLinear().domain([-20,40]).range([0,1]);

		//set up our projection (like a scale, but for two values!)
		var projection = d3.geoEquirectangular()
		.scale(width / 2 / Math.PI)
		.translate([width / 2, height / 2]);


		//set up path generator (like a scale, but for curves!)
		var path = d3.geoPath()
		.projection(projection);


		//create svg container
		var svg = d3.select("body")
		.append("svg")
		.attr("width", width)
		.attr("height", height)
		.style("background-color","#cde")
		;

		//draw maps
		d3.json("world-110m.json", function(err, geojson) {
			svg.append("path")
			.attr("d", path(geojson))
		})

		//automatically call our function at regular intervals
		var interval = setInterval(
			function(){
				drawMap();
			}, 10*1000);

		//
		function drawMap(){
			d3.json('http://api.openweathermap.org/data/2.5/group?id=' + cities + '&units=metric&appid=' + apikey, function(error, weather) {
				if (error) throw error;

				console.log(weather);

				//delete any existing circles
				svg.selectAll(".dot").remove();

				//draw a dot at each city coodinate
				svg.selectAll(".dot")
				.data(weather.list)
				.enter()
				.append("circle")
				.attr("r", function(d) { return d.wind.speed})
				.attr("cx", function(d) { return x(d.coord.lon); })
				.attr("cy", function(d) { return y(d.coord.lat); })
				.attr("fill",function(d) { return d3.interpolatePlasma(tmp(d.main.temp)); })
				.attr("stroke","#fff")
				.attr("stroke-width","1")
				.classed("dot",true)
				;

				//delete any existing label
				svg.selectAll(".label").remove();

				//draw a label at each city coodinate
				svg.selectAll(".label")
				.data(weather.list)
				.enter()
				.append("text")
				.text(function(d) { return d.name + " | " + d.main.temp})
				.attr("x", function(d) { return x(d.coord.lon)+d.wind.speed+3; })
				.attr("y", function(d) { return y(d.coord.lat)+ 3; })
				.attr("stroke", "none" )
				.attr("fill","#fff")
				.style("font-family","lato")
				.style("font-size","10px")
				.classed("label",true)
				;

			});
		};      

		//the map updates itself, but it needs to be run once when the page loads!
		drawMap();

	</script>

</body>
</html>

```
