EDAV3 Notes
================

Add elements with `.append()`
=======

``` js
<script id="s2">
d3.select("body").append("svg").attr("width", "500")
    .attr("height", "400");
    
d3.select("svg").append("rect").attr("x", "0").attr("y", "0")
    .attr("width", "500").attr("height", "400").attr("fill", "lightblue");
    
d3.select("svg").append("circle").attr("cx", "200")
    .attr("cy", "100").attr("r", "25").attr("fill", "orange");
    
d3.select("svg").append("circle").attr("cx", "300")
    .attr("cy", "150").attr("r", "25").attr("fill", "red");  
    
</script>
```

Binding data... _finally!_ (Console)
=======

Open S

``` js
var dataset = [90, 230, 140, 75, 180, 25];

var svg = d3.select("svg");

var circ = svg.selectAll("circle");

circ

circ.data(); // nothing there

circ.data(dataset); // check Elements, nothing changed

circ.data();  // now we see data

circ.attr("cx", function(d) {return d;});

circ.attr("cx", function(d) {return d/2;});

circ.attr("cx", function(d) {return d/4;}).attr("r", "10");
```

Same as above, using arrow functions:

```
circ.attr("cx", d => d);

circ.attr("cx", d => d/2);

circ.attr("r", d => d/4).attr("r", "10");
```

Store selection in a variable
=======

Console:
``` js
var svg = d3.select("svg");
svg
var a = d3.select("svg").append("circle");
a
a.attr("cx", "300").attr("cy", "200").attr("r", "15").attr("fill", "green");  
var circ=d3.selectAll("circle");
circ.attr("fill", "blue");
```


Store selection in a variable
=======

``` js
<script id="s3">
var svg = d3.select("body").append("svg")
    .attr("width", "500").attr("height", "400");
svg.append("rect").attr("x", "0").attr("y", "0")
      .attr("width", "500").attr("height", "400").attr("fill", "lightblue");
svg.append("circle").attr("cx", "250").attr("cy", "150")
    .attr("r", "20").attr("fill", "blue");
</script>
```

Adding D3 to `html` file
========================

Start with bare minimum `html` (w/ D3 link). Copy and paste the code below, or download [D3template.html](https://raw.githubusercontent.com/jtr13/D3/master/D3template.html).

``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Change the title!</title>
    <script src="https://d3js.org/d3.v4.min.js"></script>  <!-- link to D3 library -->
  </head>

  <body>
    <script>
    // JavaScript / D3 will go here
    </script>
  </body>

</html>
```

Add svg
=======

``` js
<script id="s1">
d3.select("body").append("svg").attr("width", "500")
    .attr("height", "400");
</script>
```



Practice 1
=======
Download and open [EDAV3.html](EDAV3.html)

Create the same visualization we did last class, but this time, build all the elements and execute the transitions from within the .html file:

1. Create an svg, background rectangle, and six circles, one with an id.

1. Move all circles to the right.

1. Move them back to the left and change their color.

1. Move the circle with the id to the right.

1. Move all the circles to the middle of the screen, then move them all to the same location.


Practice 2
=======
Download and open [SixBlueCircles.html](SixBlueCircles.html)

(or use [this online version](https://jtr13.github.io/D3/SixBlueCircles.html)).

Either in the Console or in the .html file bind data -- an array of exactly six values -- to the circles and use the data property to modify the circles.
