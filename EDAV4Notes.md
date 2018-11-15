EDAV4 Notes
================

Binding data
=======
### 1. Number of DOM elements = number of data values

Open a downloaded copy of [SixBlueCircles.html](https://raw.githubusercontent.com/jtr13/D3/master/SixBlueCircles.html), or use this [online version](https://jtr13.github.io/D3/SixBlueCircles.html). (Right click to open in a new tab.)

Define the following variables by executing this code in the Console:

``` js
var svg = d3.select("svg");

var dataset = [34, 123, 70, 187, 200, 324];

var circ = svg.selectAll("circle");
```

Check data binding:
``` js
circ.data();
```

You should get:
`(6) [undefined, undefined, undefined, undefined, undefined, undefined]` since we have not bound any data yet.


Now, we'll bind data to the circles:
``` js
circ.data(dataset);
```

And check the data bind again:
``` js
circ.data();
```

We can use the bound data to modify attributes. Try these one at a time:

``` js
circ.attr("cx", d => d);

circ.transition()
    .duration(2000)
    .attr("cx", d => 2*d);

circ.transition()
    .duration(2000)
    .attr("cx", d => d/2);
```

If we bind a new set of data to the DOM elements, the original set will be overwritten:

``` js
var newdata = [145, 29, 53, 196, 200, 12];

circ.data(newdata);

circ.transition()
    .duration(2000)
    .attr("cx", d => 2*d);

```

### Update, Enter, and Exit Selections
 
[UpdateEnterExit.pdf](UpdateEnterExit.pdf)



### More DOM elements than data values

Let's bind four data values to the six circles. (Note that we are not defining a separate variable for the dataset, simply entering the data array into the *select().data()* chain:

``` js
svg.selectAll("circle")
    .data([123, 52, 232, 90]);
```

Click the black triangle to view the `_enter`, `_exit`, and `_groups` fields. 


We can store the selection in a variable:

``` js
var circ = svg.selectAll("circle")
    .data([123, 52, 232, 90]);
```

Let's look at the exit selection:

``` js
circ.exit();
```

Try this:
``` js
circ.attr("fill", "red");
```

What happened and why?

Now try this:
``` js
circ.exit().attr("fill", "purple");
```

What happened and why?

What do you think this will do? Try it.

``` js
circ.exit().transition().duration(2000).remove();

```

Look again at the `circ` selection:
``` js
circ;
```

Create a new variable `circ2` and compare it to `circ`:
``` js
var circ2 = d3.selectAll("circle");

circ2;

circ2.data();
```

What's going on?




### More data values than DOM Elements
``` js
<script id="s4">

var circ = svg.selectAll("circle")
      .data([123, 52, 232, 90, 34, 12, 189, 110]);

  circ.enter()
      .append("circle")
        .attr("cx", "50")
        .attr("cy", (d, i) => i * 50 + 100)
        .attr("r", "20")
        .attr("fill", "red");

  // only acts on update selection
  circ.transition()
        .duration(3000)
        .attr("cx", "400");


</script>
```

Scenario 1: Combining update and enter selections with `.merge()`
=======

``` js
<script id="s5">
// simplified code after 3/27 class:

    var allcirc = circ  // all existing circles -- see script s1
        .data([123, 52, 232, 90, 34, 12, 189, 110])
        .enter()  // 2 placeholders
        .append("circle")  // placeholders -> circles
          .attr("cx", "50")  // acts on enter selection only
          .attr("cy", (d, i) => i * 50 + 100)
          .attr("r", "20")
          .attr("fill", "red")
	.merge(circ)  // combines enter and update selections
	
    allcirc.transition() // acts on all 8 circles
          .duration(3000)
          .attr("cx", "400")
          .attr("fill", "purple");

    allcirc.transition() // acts on all 8 circles
        .delay(3000)
        .duration(3000)
        .attr("cx", "50");

</script>
```

Scenario: no DOM elements exist
=======
### data / enter / append sequence

``` js
<script id="s6">

  var specialdata = [100, 250, 300];

  var bars = svg.selectAll("rect")
      .data(specialdata)
      .enter()
      .append("rect")
        .attr("x", d => d)
        .attr("y", d => d)
        .attr("width", "50")
        .attr("height", "30")
        .attr("fill", "green");

  d3.selectAll("circle").remove();


</script>
```

Practice 1: Horizontal Bar Chart
=======



Submit / view solutions here: [ExerciseSolutions.md](ExerciseSolutions.md)

1. Create a new html file (try to recreate the template without looking!). Add a script that adds an svg element and horizontal bars of the lengths (in pixels) specified in `bardata`. Create the bars with the data / enter / append sequence.

    `var bardata = [300, 100, 150, 225, 75, 275];`
    
    *Note: it's best to work in the Console for the following so you don't have to sequence the changes.*

1. Change the data to any six other values and update the lengths of the bars.

1. Bind a new dataset, `newbardata` to the bars, update the bar lengths, and remove any extra bars.

    `newbardata = [250, 125, 80, 100];`

1. Bind a new dataset, `reallynewbardata`, to the bars, then add additional bars so each data value has a bar. Make the outline (stroke) of the new bars a different color.

    `reallynewbardata = [300, 100, 250, 50, 200, 150, 325, 275];`

1. Use `.merge()` to combine the update and enter selections into one selection and then transition the height of all of the bars to half their current height.

1. Add text labels inside the bars at the right end with the length of the bar in pixels.</p></li>
