###Interval-Based Querying

---

We can ask Javascript to regularly run our `updateMap()` function based on a millisecond interval.

```
	var interval = setInterval(
		function(){
			updateMap();
		},
	5000);
```

This will run the `updateMap` function every 5 seconds.

The map now automatically asks the API for new data regularly, keeping itself up-to-date. The problem, observable after the first new data flows into the system, is that new geometry is drawn on top of old geometry.

View the [complete code](complete.md) to see the fix which involves a line of code to remove all existing circles *before* drawing new ones. 

```
	svg.selectAll(".dot").remove();
```

We may also want to prevent the page from [caching](cache.md), as in some common scenarios our script may fail to grab new data.
