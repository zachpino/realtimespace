###Accessing Data

D3 make it easy to look at a dataset file, and get information out of it!

```
// Get the data
d3.csv("data.csv", function(error, data) {
  if (error) throw error;

  // format the data
  data.forEach(function(d) {
      d.lat = +d["Latitude"];
      d.long = +d["Longitude"];
      d.pop = +d["2015Pop"];
  });
```

Here we are naming our dataset file, and giving some new names to our dataset's contents. The `+` character is ensuring that D3 treat these as numbers.

We can now use the data to create some svg circles.

```
<html>
<head>

<body>

<!-- load the d3.js library -->     
<script src="https://d3js.org/d3.v4.min.js"></script>

<script>

//define our block size variables
var width = 1000;
var height =  600;

// set the ranges
var x = d3.scaleLinear().domain([-180,180]).range([0, width]);
var y = d3.scaleLinear().domain([-90,90]).range([height, 0]);


// append the svg obgect to the body of the page
var svg = d3.select("body").append("svg")
    .attr("width", width)
    .attr("height", height)
    .style("background-color","#cde")
;

// Get the data
d3.csv("data.csv", function(error, data) {
  if (error) throw error;

  // format the data
  data.forEach(function(d) {
      d.lat = +d["Latitude"];
      d.long = +d["Longitude"];
      d.pop = +d["2015Pop"];
      d.city = d["City"];
      d.country = d["Country"];
  });

  // Add the scatterplot
  svg.selectAll("dot")
      .data(data)
      .enter()
      .append("circle")
      .attr("r", function(d) { return d.pop / 1000; })
      .attr("cx", function(d) { return x(d.long); })
      .attr("cy", function(d) { return y(d.lat); })
      .attr("stroke","cyan")
      .attr("stroke-width","1")
      .append("title").text(function(d) { return d.city + ", " + d.country; })
;

});

</script>
</body>
```
