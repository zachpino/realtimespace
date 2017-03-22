###Update
---

Now that [new data](enter.md) is smoothly animated into our dataset, we might want to give some feedback to viewers of the visualization that the *unchanged* data is in fact live. To do this, we can add some familiar code to our `drawDots()` function.

Place this code below the `//enter` block.

```
//update
					dots
					.transition()
					.duration(1000)
					.attr("r", function(d){return d.size*2})
					.attr("cx",function(d){return d.x})
					.attr("cy",function(d){return d.y})
					.transition()
					.duration(1000)
					.attr("r", function(d){return d.size})
					;
 ```
 
 Over two seconds, this code runs a *compound transition* on our elements. Any pre-existing datapoint grows to twice its original size over one second, and then shrinks back down to normal size over the second second. Add as many transitions as you would like for feedback purposes!
 
