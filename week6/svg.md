###Adding an SVG container

---

We can use D3 to find the `body` tag of the [base html page](structure.md), and insert an `<svg>` element to hold our visualization. Place this in the empty script tag in the body of the page.

```
var width = 960;
var height = 600;
    
var svg = d3.select("body")
		.append("svg")
		.attr("width", width)
		.attr("height", height)
		.style("background-color","#cde")
		;
```

We can now begin to do the math necessary to map dataset values to pixel coordinates with [scales](scale.md).
