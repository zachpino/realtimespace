###Mapping Scales
---

Let's setup some utility scales to convert the data's `lat` and `lon` coordinates to more useful pixel values based on the `width` and `height` variables of our [svg container](svg.md). 

We can also setup a scale to map our celsius temperatures to a *parameterized* 0 - 1 range. This is important for some color work we will do later, as sequential scales in D3 expect parameterized data.

Remember, `domain = input boundaries` and `range = output boundaries`.

```    
    var x = d3.scaleLinear().domain([-180,180]).range([0, width]);
		var y = d3.scaleLinear().domain([-90,90]).range([height, 0]);
		var tmp = d3.scaleLinear().domain([-20,40]).range([0,1]);
```

After setting up these scales, let's [query the API](query.md) with D3.
