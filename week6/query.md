###Querying the Open Weather Map API
---

With [scale utility functions](scale.md) out of the way, let's get into the data with D3!

```
    var apikey = "###########################";
    
      d3.json('http://api.openweathermap.org/data/2.5/group?id=524901,703448,2643743&units=metric&APPID=' + apikey, function(error, weather) {
			  if (error) throw error;
        
        console.log(weather)
    });
```

Replace the `group` values with the cities you would like to map and paste in your API key.

Check the console and evaluate if the data came through! You should see a set of several Javascript objects ready for your use.

Let's [draw some circles](draw.md) with that data.
