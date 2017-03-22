###Setup
---

A base html file with the following code will be the foundation for the data-derived animations produced this week.

The only new/weird thing is a button placed on the page, which calls a function `drawDots()` which has not yet been defined. We will use this to manually update the page. Similarly, commented at the bottom of the script is our standard automatic update function.


```
<html>
<head>
	<title>Transitions and Update Patterns</title>

	<style>

	</style>

</head>
<body>

	<button onclick="drawDots()">Click me</button>


	<script src="https://d3js.org/d3.v4.min.js"></script>


	<script>

		var width = 1000;
		var height = 1000;

		//create svg container
		var svg = d3.select("body")
		.append("svg")
		.attr("width", width)
		.attr("height", height)
		.style("background-color","#ccc")
		;


		//on page load
		d3.json("mock.json", function(error,data) {
			svg.selectAll(".dots")
			.data(data)
			.enter()
			.append("circle")
			.attr("cx",function(d){return d.x})
			.attr("cy",function(d){return d.y})
			.attr("r", function(d){return d.size})
			.attr("fill",function(d){return d.color})
			.classed("dots", true)
			;
		});


		/*
		//automatically call our function at regular intervals
		var interval = setInterval(
			function(){
				drawMap();
			}, 5*1000);

		*/
		</script>

	</body>
	</html>
```


This data visualization code requires a placeholder dataset `mock.json` which was generated by the wonderful [mockaroo](http://www.mockaroo.com). Check it out for all of your fake data needs!

It is a five-dimensional dataset with a fake city name, x and y coordinates, a color, and a size variable.

```
[
{"name":"Smolyan","x":869,"y":137,"color":"#7d785e","size":6},
{"name":"Tarica","x":261,"y":376,"color":"#5f567c","size":10},
{"name":"Lobos","x":15,"y":520,"color":"#226c42","size":7},
{"name":"Estribeiro","x":584,"y":184,"color":"#a64081","size":18},
{"name":"Al Wuday‘","x":91,"y":298,"color":"#4f8904","size":5},
{"name":"Sabóia","x":246,"y":707,"color":"#d87ece","size":4},
{"name":"Xiabao","x":822,"y":614,"color":"#30c593","size":15},
{"name":"Manhush","x":735,"y":444,"color":"#6dc6a5","size":8},
{"name":"São Lourenço da Mata","x":673,"y":863,"color":"#814f02","size":19},
{"name":"Daixi","x":108,"y":735,"color":"#fe70f2","size":3}
]
```