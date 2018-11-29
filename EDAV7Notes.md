EDAV7 Notes
================

## Axes

Add x-axis
[EDAV7_1_axes.html](EDAV7_1_axes.html)

## Interactivity

[Interactivity.pdf](Interactivity.pdf)

## Transitions

[Transitions.pdf](Transitions.pdf)

### First attempt

[EDAV7_2_transitions.html](EDAV7_2_transitions.html)

**Of note:** 

* Rather than smoothly transitioning off to the left, all bars are resized when "Remove bar (left)" is clicked

* When "Remove bar (right) is clicked, the bar on the right immediately disappears, and then the remaining bars transition to their new places to the right.

## Object constancy

[ObjectConstancy.pdf](ObjectConstancy.pdf)

[EDAV7_3_obj_constancy.html](EDAV7_3_obj_constancy.html)

**Of note:** 

* Bars now smoothly transition off to the left and right

### Practice joining data by key

Download and open [DataBindwithKeys.html](DataBindwithKeys.html)

(or open [this online version](https://jtr13.github.io/D3/DataBindwithKeys.html)) in a new tab.


Try the following:

1.

``` js
var svg = d3.select("svg");

var dataset = [{key: 12, x: 100, y: 200},
              {key: 16, x: 250, y: 300}];
              
svg.selectAll("text")
  .data(dataset, d => d.key)
  .exit()
  .remove();
```

Then:

``` js
svg.selectAll("text")
  .attr("x", d => d.x)
  .attr("y", d => d.y);
```

2. 

(Refresh)

``` js
var dataset = [{key: 23, x: 300, y: 150},
              {key: 5, x: 450, y: 270}];
              
var databind = svg.selectAll("text")
  .data(dataset, d => d.key)

databind.exit().remove();
```

Then:
``` js
databind.enter().append("text")
  .attr("x", d => d.x)
  .attr("y", d => d.y)
  .text(d => `key: ${d.key}`);
```

3. Experiment with other data binds.

