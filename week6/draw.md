###Drawing with Data
---

Within your `d3.json` code block, add the following code to produce a circle for each city, colored by its temperature. You can use the same logic to do just about anything with this dataset and svg circles!

```
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
 ```
 
This code will automatically query the API whenever you reload the page, but it would be nice to have some other way of [manually updating](button.md) the page.
