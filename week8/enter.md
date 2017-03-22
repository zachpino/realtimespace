###Entering New Data
---
The [setup visualization](setup.md) should render some random dots to the screen.

What happens, however, when the dataset grows new elements? Currently, the visualization does not react to changes in the data.

Let's fix that! Place this code below the `//on page load` block

```
function drawDots(){

	d3.json("mock.json", function(error,data) {

					//save selection as variable
					var dots = svg.selectAll(".dots")
					.data(data);


					//enter
					dots
					.enter()
					.append("circle")
					.attr("cx",function(d){return d.x})
					.attr("cy",function(d){return d.y})
					.attr("r", 0)
					.classed("dots", true)
					.transition()
					.duration(5000)
					.attr("r", function(d){return d.size})
					.attr("fill",function(d){return d.color})
					;
          
          });
};      
```

This code draws a new circle for all new datapoints, and animates them from a radius of zero black circle to their data-derived size and color over a period of time defined by `duration`.

Add an element to `mock.json` and hit the button on the page to see the animated results.

This works fine, but it might be nice to visualize that the other static data points are in fact [updating](update.md), and not just frozen in place.
