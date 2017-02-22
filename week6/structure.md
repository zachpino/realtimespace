###Base Page Structure
---

We have [our data](analysis.md). But, as always, our page needs to be valid html and inlude a reference to the D3 library. This can be done locally, or on your server.

```
<html>
<head>
	<title>Realtime Weather Map</title>
  <style
    /*page styles go here*/
  </style>
</head>

<body>
	<script src="https://d3js.org/d3.v4.min.js"></script>

  <script>
	  //d3 code goes here
  </script>

</body>
</html>
```

We can now use D3 to inject an [SVG container](svg.md).
