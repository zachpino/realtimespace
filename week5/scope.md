###Scoping Data

-----

A fundamental aspect of working with D3 is the idea *scales*, which use *domains* and *ranges* to manage visualization intent. 

- A *domain* is the boundaries of our data. For instance, if our dataset comprised timestamps collected all day, our domain might be -12 to 12.
- A *range* is the boundaries of our data's intended representation. If we wanted those timestamps to fit into a 100px graphic, our range would be 0 to 100.

D3 uses domains and ranges to map our data to our screen's coordinates.

```
<html>
<head>
  <style> 
  </style>
</head>

<body>

    <script src="https://d3js.org/d3.v4.min.js"></script>

    <script>
    
      //make size variables
      var width = 1000;
      var height =  600;

      //create svg container
      var svg = d3.select("body").append("svg")
      .attr("width", width)
      .attr("height", height)
      .style("background-color","#cde")
      ;
      
      // set the intended range
      var x = d3.scaleLinear().range([0, width]);
      var y = d3.scaleLinear().range([height, 0]);

      // scale the domain of the data
      x.domain([-180,180]);
      y.domain([-90,90]);

    </script>
</body>
</html>
```
