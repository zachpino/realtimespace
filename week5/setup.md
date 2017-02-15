###Starting Code

Let's begin this introduction to javascript with the following recognizable code.

```
<html>
<head>
  <style> 
  </style>
</head>

<body>

	<script src="https://d3js.org/d3.v4.min.js"></script>
  
</body>
</html>

```

This code should be familiar. We have `head` and `body` tags nested inside of the `html` container, and a `style` tag inside of `head` ready for CSS rules.

The new line here is the `<script>` tag. This is a link the [D3 data visualization library](http://www.d3js.org), a collection of functions and helpers that ease the work of producting data visualizations. Like `<img>` tags, the script tag takes a `src=""` attribute setting the path to the file. Rather than downloading this file directly, we are going to point browsers to the file on the D3 website so they always get the most up-to-date version.

By placing this line in our code, we are effectively including all of that linked code in our page.

Now, we can look at the data we plan to plot with this library!

