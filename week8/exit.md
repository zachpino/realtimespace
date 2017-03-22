###Exiting Data
---

Animating [added](enter.md) and [updated](update.md) data is easy. So too is removing elements for data that has fallen out of the dataset.

Below the `//update` block, we can add this code to remove now empty datapoints.

```
					//exit
					dots
					.exit()
					.transition()
					.duration(3000)
					.ease(d3.easeBounceOut)
					.attr("cy", height)
					.style("fill-opacity", 0)
					.remove();
```

This code, over 3 seconds, removes all circles for any data-derived element on the page that no longer exists in the dataset. The circles move to the bottom of the svg container, fades out, and is removed.

Note the `.ease` method. This allows for non-linear animation. Check out the [d3 reference](https://github.com/d3/d3-ease) for other options.

Now, take this structure of `enter`,`update`, and `exit` and create your own animated visualizations!
