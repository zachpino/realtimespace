###SVG Container

To begin our exploration of D3, let's add a second `<script>` tag to our `<body>`, this one though, will not have a `src` attribute. Inside of it, we will place our first lines of Javascript!

```
<html>
<head>
  <style> 
  </style>
</head>

<body>

    <script src="https://d3js.org/d3.v4.min.js"></script>
    
      //make size variables
      var width = 1000;
      var height =  600;
      
      //create svg container
      var svg = d3.select("body").append("svg")
      .attr("width", width)
      .attr("height", height)
      .style("background-color","#cde")
      ;
    
    <script>
    
    
    </script>
</body>
</html>

```

The order and placement here is important. If our D3 code is nested *after* our code, our calls will fail! Browers load files and scripts from top to bottom, so we need to load D3 *before* we can use it.

Javascript is a *weakly-typed* programming language. We can make and use data without knowing what kind of data it is. Normally, in most programming languages, you would need to declare if the data you are using is an integer or boolean datatype. Javascript doesn't care! This make it easier on beginners, but can cause hard-to-diagnose problems with more complex applications.

Here, we are making two variables to store some important information -- how big we want our visualization to be in pixels in both dimensions.

Afterwards, we are using those variables to create an `<svg>` element. SVG is a lightweight scripting language for drawing vector graphics that D3, web browsers, and Adobe Illustrator speak natively. Take a look at the [reference](https://developer.mozilla.org/en-US/docs/Web/SVG/Element) to see what is possible.
