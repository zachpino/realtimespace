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

The map now automatically asks the API for new data regularly, keeping itself up-to-date.

View the [complete code](complete.md).
