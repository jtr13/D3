EDAV 5 SOLUTIONS
==============

### Sample standard deviation

``` js
var x = [3, 5, 7, 8, 9]
```

Deviations from mean:

``` js
var dev = x.map(d => d - d3.mean(x))
```

Squared deviations:

``` js
var devsq = dev.map(d => Math.pow(d, 2));
```

Sum of squared deviations:

``` js
var sumdevsq = d3.sum(devsq);
```

Sample variance:

``` js
var variance = sumdevsq/(x.length - 1);
```

Sample standard deviation:

``` js
var sd = Math.sqrt(variance);
```

OR

``` js
var sd = Math.sqrt(d3.sum(x.map(d => Math.pow(d - d3.mean(x), 2)))/(x.length-1));
```

or 
``` js
d3.deviation(x);
```

:-)
