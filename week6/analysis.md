###Dataset Analysis

---

There are many examples on the [Open Weather Map](data.md) [Realtime API](http://openweathermap.org/current) documentation page for accessing weather data in different ways.

We will be querying the API for several cities based on their IDs, which can be referenced in this [index](http://bulk.openweathermap.org/sample/city.list.json.gz) (beware: it is a large download). Select a few cities to use in this exercise map and copy their IDs.

To formulate an API request of multiple cities by ID, the query would look like the following.

```
http://api.openweathermap.org/data/2.5/group?id=4887398,3936456,344979,1821306&units=metric&APPID=#########################
```

The four values in the group key reference `Chicago, US`, `Lima, Peru`, `Addis Ababa, Ethiopia` and `Phnom Penh, Cambodia`. Note that, in a free account, we can access only 20 cities per request.

The `units` key allows us to specify `metric` or `imperial`. If you leave out the `units` key, the values will be returned in degrees Kelvin and in base SI units (barometric data will be in grams / square meter, wind speed will be in meters/second...).

Finally, we need to include our api key as an `APPID` value.

Construct some API requests and check the results in your browser. Be careful, you can only make 60 requests per minute.

Now, we can look at the results.

```
{"cnt":4,"list":[{"coord":{"lon":-87.65,"lat":41.85},"sys":{"type":1,"id":961,"message":0.1895,"country":"US","sunrise":1487766878,"sunset":1487806394},"weather":[{"id":741,"main":"Fog","description":"fog","icon":"50d"},{"id":701,"main":"Mist","description":"mist","icon":"50d"},{"id":300,"main":"Drizzle","description":"light intensity drizzle","icon":"09d"}],"main":{"temp":11.55,"pressure":1009,"humidity":93,"temp_min":11,"temp_max":12},"visibility":402,"wind":{"speed":4.6,"deg":210},"clouds":{"all":90},"dt":1487769060,"id":4887398,"name":"Chicago"},{"coord":{"lon":-77.03,"lat":-12.04},"sys":{"message":0.1581,"country":"PE","sunrise":1487761770,"sunset":1487806404},"weather":[{"id":800,"main":"Clear","description":"Sky is Clear","icon":"01d"}],"main":{"temp":21.46,"temp_min":21.46,"temp_max":21.46,"pressure":877.99,"sea_level":1024.39,"grnd_level":877.99,"humidity":58},"wind":{"speed":1.17,"deg":214.5},"clouds":{"all":0},"dt":1487770271,"id":3936456,"name":"Lima"},{"coord":{"lon":38.75,"lat":9.02},"sys":{"type":1,"id":6338,"message":0.1601,"country":"ET","sunrise":1487734873,"sunset":1487777734},"weather":[{"id":802,"main":"Clouds","description":"scattered clouds","icon":"03d"}],"main":{"temp":24,"pressure":1023,"humidity":23,"temp_min":24,"temp_max":24},"visibility":10000,"wind":{"speed":2.1,"deg":130},"clouds":{"all":40},"dt":1487768400,"id":344979,"name":"Addis Ababa"},{"coord":{"lon":104.92,"lat":11.56},"sys":{"type":1,"id":7872,"message":0.1716,"country":"KH","sunrise":1487719106,"sunset":1487761743},"weather":[{"id":801,"main":"Clouds","description":"few clouds","icon":"02n"}],"main":{"temp":30,"pressure":1009,"humidity":70,"temp_min":30,"temp_max":30},"visibility":10000,"wind":{"speed":2.6,"deg":150},"clouds":{"all":20},"dt":1487768400,"id":1821306,"name":"Phnom Penh"}]}
```
Look at all that data! Within the `list` array sits four entities, each with several subarrays of data available. 

- The `coord` subarray gives longitude and latitude of the city. `sys` gives country code and sunrise/sunset time in GMT.
- `weather` gives access to an icon (which can be pulled from a separate dataset) as well as general descriptors of the current weather.
- `main` shows all sorts of quantitative data including temperature and humidity.
- `visibility`, `wind`, and `clouds` all contain straightforward data on the current conditions.

We will need to understand how this data is nested to get anywhere with our visualization. For instance, to get a city's current high temperature, we would need to access (in dot notation):

```
data.list.main.temp_max
```
