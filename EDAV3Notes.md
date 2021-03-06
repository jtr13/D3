EDAV3 Notes
================

<!-- IF THIS IS A .MD FILE, DO NOT EDIT!!!! -->

## Add elements with `.append()`

<!-- Open `D3template.html` in Chrome. -->

``` js
> d3.select("body").append("svg").attr("width", "500")
    .attr("height", "400");
    
> d3.select("svg").append("rect").attr("x", "0").attr("y", "0")
    .attr("width", "500").attr("height", "400").attr("fill", "lightblue");
    
> d3.select("svg").append("circle").attr("cx", "200")
    .attr("cy", "100").attr("r", "25").attr("fill", "orange");
    
> d3.select("svg").append("circle").attr("cx", "300")
    .attr("cy", "150").attr("r", "25").attr("fill", "red");  
```

## Binding data… *finally\!* (Console)

Open your local copy of `SixBlueCircles.html` in Chrome, or use the
[online version](https://jtr13.github.io/D3/SixBlueCircles.html) (right
click to open in a new tab).

Bind
data:

``` js
> d3.select("svg").selectAll("circle").data([90, 230, 140, 75, 180, 25]);
```

Check data binding:

``` js
> d3.select("svg").selectAll("circle").data();
```

Set x-coordinate of each circle to data value using arrow function:

``` js
> d3.select("svg").selectAll("circle").attr("cx", d => d);
```

Set x-coordinate of each circle to data value using traditional
JavaScript
function:

``` js
> d3.select("svg").selectAll("circle").attr("cx", function(d) {return d;});
```

## Store selection in a variable

Open `SixBlueCircles.html` in Chrome, or use the [online
version](https://jtr13.github.io/D3/SixBlueCircles.html) (Right click to
open in a new tab.)

Store the `svg` selection:

``` js
> var mysvg = d3.select("svg");
```

## 

Note: the JavaScript community is moving toward using `let` and `const`
instead of `var`; we will stick with `var` as in *IDVW*.

## 

Examine `mysvg`:

``` js
> mysvg;
```

\-\> Look at the `_groups` and `_parents` objects.

## 

Use the selection to create a new
element:

``` js
> mysvg.append("circle").attr("cx", "250").attr("cy", "250").attr("r", "50")
  .attr("fill", "green");
```

Store circle selection in a variable:

``` js
> var dataset = [90, 230, 140, 75, 180, 25];

> var svg = d3.select("svg");

> var circ = svg.selectAll("circle");

> circ;
```

## Bind data using stored selections

``` js
> circ.data(); // nothing there
```

You should get: `(6) [undefined, undefined, undefined, undefined,
undefined, undefined]` since we have not bound any data yet.

``` js
> circ.data(dataset); // check Elements, nothing changed

> circ.data();  // now we see data
```

## Modify elements w/ stored selections, bound data

``` js
> circ.attr("cx", function(d) {return d;});

> circ.attr("cx", function(d) {return d/2;});

> circ.attr("cx", function(d) {return d/4;}).attr("r", "10");
```

## Arrow functions

Same as above, using arrow functions:

``` js
> circ.attr("cx", d => d);

> circ.attr("cx", d => d/2);

> circ.attr("r", d => d/4).attr("r", "10");
```

Note that if we bind a new set of data to the DOM elements, the original
set will be overwritten:

``` js
> var newdata = [145, 29, 53, 196, 200, 12];

> circ.data(newdata);

> circ.transition()
    .duration(2000)
    .attr("cx", d => 2*d);
```

## Practice 1

With `SixBlueCircles.html` open in Chrome, practice binding data to the
circles and modifying the circles based on the data as in the examples
above.

## Adding D3 to `html` file

``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Change the title!</title>
    <script src="https://d3js.org/d3.v5.min.js"></script>  <!-- link to D3 library -->
  </head>

  <body>
    <script>
    // JavaScript / D3 will go here
    </script>
  </body>

</html>
```

## Add svg

``` js
<script>
d3.select("body").append("svg").attr("width", "500").attr("height", "400");
</script>
```

## Add a circle

``` js
<script>
d3.select("body").append("svg").attr("width", "500").attr("height", "400");

d3.select("svg").append("circle").attr("cx", "200").attr("cy", "250")
  .attr("r", "20").attr("fill", "red");
</script>
```

## Practice 2

Start with bare minimum `html` (w/ D3 link):
[D3template.html](https://raw.githubusercontent.com/jtr13/D3/master/D3template.html).

Open the file in your text editor. Then add code to the `<script>`
section to create an svg and then add `svg` elements to it.
