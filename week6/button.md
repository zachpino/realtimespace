###Updating Data with a Button
---

Let's add a button the body of the page above the scripts which [draw the circles](draw.md).
```
	<button id="update">Update</button>
```

Now, wrap the `d3.json` block with a function name as in the following

```
function updateMap(){
			d3.json('http://api.openweathermap.org/data/2.5/group?id=524901,703448,2643743&units=metric&APPID=#################', function(error, weather) {
          ...
			});
	}
```

Now, whenever `updateMap()` is called, the map will update its json dataset!

We can use very simple code to fire that function whenever our new button is pressed. This should be placed above the function declaration we added above.

```
d3.select("#update").on("click", function(){
		updateMap();
});
```

This binds the click event of our button with `id` of `update` to a D3 expression, which redraws our map with more up-to-date data!

