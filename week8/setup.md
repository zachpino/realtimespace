###Setup
---

A base html file with the following code will be the foundation for the data-derived animations produced this week.

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
