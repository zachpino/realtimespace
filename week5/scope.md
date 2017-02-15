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
      var x = d3.scaleLinear().domain([-180,180]).range([0, width]);
      var y = d3.scaleLinear().domain([-90,90]).range([height, 0]);
      
    </script>
</body>
</html>
```

We justr created 2 scales, one for x and one for y!

We know that our data fits into -180 to 180 for longitude, and -90 to 90 for latitude. We want our visualization to fit into specific pixels on our website, from 0 to the `width` and `height` variables. 

Take a look at the documentation for d3 scales, where you will also see all the [other kinds of scales](https://github.com/d3/d3-scale) available. 

Let's use those scales. Add this line at the bottom of your script.

```
console.log(x(90));
```

In your web console, you should find the pixel mapping for a longitude of 90!

Now, let's ask d3 to look at our data.
