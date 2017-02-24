Don't forget to define your apikey!

```
<html>
<head>
	<title>Realtime Weather Map</title>
</head>
<body>
	<script src="https://d3js.org/d3.v4.min.js"></script>


	<button id="update">Update</button>

	<script>
		var apikey = "######################";
		var cities = "4887398,361058,6542286,993800,4140963,256637,3941584,5391959,1857910,1642911,2624652,6547294,1819730,4553433"
		var width = 960;
		var height = 600;

		// set the domain and ranges for latitude and longitude
		var x = d3.scaleLinear().domain([-180,180]).range([0, width]);
		var y = d3.scaleLinear().domain([-90,90]).range([height, 0]);
		var tmp = d3.scaleLinear().domain([-20,40]).range([0,1]);

		var svg = d3.select("body")
		.append("svg")
		.attr("width", width)
		.attr("height", height)
		.style("background-color","#cde")
		;

		var interval = setInterval(
			function(){
				updateMap();
			},
			5000);

		function updateMap(){
			d3.json('http://api.openweathermap.org/data/2.5/group?id=524901,703448,2643743&units=metric&APPID=' + apikey, function(error, weather) {
				if (error) throw error;

				console.log(weather);


		      		svg.selectAll(".dot").remove();
		
				svg.selectAll(".dot")
				.data(weather.list)
				.enter()
				.append("circle")
				.attr("r", function(d) { return  10})
				.attr("cx", function(d) { return x(d.coord.lon); })
				.attr("cy", function(d) { return y(d.coord.lat); })
				.attr("fill",function(d) { return d3.interpolatePlasma(tmp(d.main.temp)); })
				.attr("stroke","#fff")
				.attr("stroke-width","1")
				.classed("dot",true)
				;

			});
		}


	</script>

</body>
</html>
```
