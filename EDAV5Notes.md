EDAV5 Notes
================

### Functions

Download and open [HorizontalBarChart.html](HorizontalBarChart.html)

(or use [this online version](https://jtr13.github.io/D3/HorizontalBarChart.html)).

Create a function in the Console:
``` js
function changedata(data) {
  d3.select("svg")
    .selectAll("rect")
    .data(data)
    .attr("width", d => d);
    }
```

Test it out:
``` js
changedata([258, 373, 278, 9, 72, 96]);
```

What happens if there are too many data values?

``` js
changedata([196, 360, 283, 390, 46, 56, 152]);
```


Let's use the enter selection to add new bars in this case:

``` js
function changedata(data) {
  var bars = d3.select("svg") 
    .selectAll("rect")
    .data(data);    // bars is the update selection
    
  bars.enter()
    .append("rect")
      .attr("x", "30")  // until merge, acts on
      .attr("y", (d, i) => i * 50) // enter selection only
      .attr("height", "35")  
      .attr("fill", "lightgreen")
    .merge(bars) // merge in the update selection
      .attr("width", d => d); // acts on all bars
  }
```

What happens if we have more bars than data values?

``` js
changedata([325, 116, 25]);
```

Let's add to the function to remove the extra bars in this case:

``` js
function changedata(data) {
  var bars = d3.select("svg") 
    .selectAll("rect")
    .data(data);    // bars is the update selection
    
  bars.enter()
    .append("rect")
      .attr("x", "30")  // until merge, acts on
      .attr("y", (d, i) => i * 50) // enter selection only
      .attr("height", "35")  
      .attr("fill", "lightgreen")
    .merge(bars) // merge in the update selection
      .attr("width", d => d); // acts on all bars
      
  bars.exit()
    .remove();
  }
```

Try:
``` js
changedata([271, 49, 389]);
```

A fancy exit:
``` js
function changedata(data) {
  var bars = d3.select("svg") 
    .selectAll("rect")
    .data(data);    // bars is the update selection
    
  bars.enter()
    .append("rect")
      .attr("x", "30")  // until merge, acts on
      .attr("y", (d, i) => i * 50) // enter selection only
      .attr("height", "35")  
      .attr("fill", "lightgreen")
    .merge(bars) // merge in the update selection
      .attr("width", d => d); // acts on all bars
      
  bars.exit()
    .attr("fill", "red")
    .transition()
    .duration(2000)
    .attr("width", "0")
    .remove();
  }
```

``` js
changedata([234, 129, 432, 286, 49, 372]);

changedata([401, 23, 173]);
```

VOILA! We have created the D3 General Update Pattern!

More examples from Mike Bostock (creator of D3):

[General Update Pattern, I](https://bl.ocks.org/mbostock/3808218)

[General Update Pattern, II](https://bl.ocks.org/mbostock/3808221)

[General Update Pattern, III](https://bl.ocks.org/mbostock/3808234)

It is covered in *IDVW* in the "Other Kinds of Data Updates" section on pp. 178-186 in Chapter 9. (The earlier part of Chapter 9 deals with data updates in which the number of DOM elements remains the same.)

**Note that the General Update Pattern changed with D3 Version 4 so avoid examples from Version 3.**


### General Update Pattern

Also available here: [EDAV5_1.html](EDAV5_1.html)

``` js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>EDAV5_1</title>
    <script src="https://d3js.org/d3.v4.min.js"></script>
  </head>

  <body>

    <script id="s1">

// Create svg and initial bars

var svg = d3.select("body")
  .append("svg")
    .attr("width", "500")
    .attr("height", "400");

var bardata = [300, 100, 150, 225, 75, 275];

var bars = svg.selectAll("rect")
  .data(bardata);

bars.enter().append("rect")
  .attr("x", "30")
  .attr("y", (d, i) => i*50)
  .attr("width", d => d)
  .attr("height", "35")
  .attr("fill", "lightgreen");

// General Update Pattern

function update(data) {

  var bars = svg.selectAll("rect")    // data join
    .data(data);

    bars.enter()
      .append("rect")    // add new elements
        .attr("x", "30")
        .attr("y", (d, i) => i*50)
        .attr("width", d => d)
        .attr("height", "35")
        .attr("fill", "yellow")
      .merge(bars)    // merge
        .transition()
        .duration(2000)
        .attr("width", d => d)
        .attr("fill", "orange");

    bars.exit().remove();    // remove extra elements
    }

    </script>

  </body>

</html>
```

### Practice 1

Open [EDAV5_1.html](EDAV5_1.html) locally and practice running the `update()` function with different datasets in the Console.

For example:
``` js
update([100, 200, 300]);
```

### Practice 2

Change the bar chart to a vertical bar chart.

Solution: [EDAV5_2.html](EDAV5_2.html)

### Practice 3

Add "add" and "remove" buttons.

Solution: [EDAV5_3.html](EDAV5_3.html)

*Hint for 4 & 5: Take out the transitions and get the scales working. Then, if you want, add transitions back in.*

### Practice 4

Up to this point, we have assumed one-to-one correspondence between pixels and data values.  Scales allow flexibility in mapping data values to pixels. Add an ordinal scale to map the position of the bars appropriately given the width of the `svg` element, using `d3.scaleBand()`.

``` js
 var xScale = d3.scaleBand()
     .domain([...])
     .range([...]);
```

See: *IDVW*, Chapter 9, pp. 150-153  

Solution: [EDAV5_4_scaleBand.html](EDAV5_4_scaleBand.html)

### Practice 5

Add a linear scale for the y-axis using `d3.scaleLinear()`, so data will be scaled appropriately to the height of the `svg` element.

``` js
var yScale = d3.scaleLinear()
    .domain([...])
    .range([...]);
```

See: *IDVW*, Chapter 7 (Note that our dataset is one-dimensional so we only have `d`, not `d[0]` and `d[1]`.)

Solution: [EDAV5_5_scaleLinear.html](EDAV5_5_scaleLinear.html)
