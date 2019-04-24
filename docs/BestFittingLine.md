<script src="https://d3js.org/d3.v4.min.js"></script>

<div style="width: 600px">
<h3>Estimate the best fitting line</h3> 
      
<p>Drag the endpoints of the blue line to estimate the best fitting line through the data points. Then click the button to see how you did.</p>  
</div>   

<p>
<button type="button" onclick="bestfit()">Best fitting line</button>
</p>


<script type="text/javascript">

//Width and height of svg
  var w = 500;
  var h = 500;
  var padding = 30;
			
// axis min / max
  var xmin = -50;
  var xmax = 50;
  var ymin = -50;
  var ymax = 50;
          
          
// colors  
  var backgroundcolor = "#EDF5E1";  

// https://rdrr.io/cran/ggthemes/man/colorblind.html    
  var circlecolor = "#CC79A7";   
  var dragcolor = "#56B4E9";
  var bestlinecolor = "#0072B2";      
        
		
//		Scale functions

  var xScale = d3.scaleLinear()
								 .domain([xmin, xmax])
								 .range([padding, w - padding * 2]);

  var yScale = d3.scaleLinear()
								 .domain([ymin, ymax])
								 .range([h - padding, padding]);
								 		 

//Define X axis
  var xAxis = d3.axisBottom()
							  .scale(xScale)
							  .ticks(5);

//Define Y axis
  var yAxis = d3.axisLeft()
							  .scale(yScale)
							  .ticks(5);
        
//Define line generator
        
  var mylinegen = d3.line()
                    .x(d => xScale(d[0]))
                    .y(d => yScale(d[1]));

//Create SVG element
  var svg = d3.select("body")
						  .append("svg")
			  			.attr("width", w)
			  			.attr("height", h);			
			    				
  svg.append("rect")
     .attr("width", w)
     .attr("height", h)
     .attr("fill", backgroundcolor);    				
			
//Create X axis
  svg.append("g")
     .attr("transform", `translate(0, ${yScale(0)})`)
     .call(xAxis);
			
//Create Y axis
  svg.append("g")
     .attr("transform", `translate(${xScale(0)}, 0)`)
     .call(yAxis);
        
  d3.select("body")
    .append("h3")
    .attr("id", "bestline")
    .text("");    
        
  var m = d3.randomUniform(2)()-1;  
        
  var myrandom = d3.randomNormal(0, 15);   
			
  var n = 100;			
			    				
  var xcoord = d3.range(n).map(d => myrandom());

  var dataset = xcoord.map(d => [d, m*d + (1-m)*myrandom()]);		
        
// starting endpoints of draggable line    
  var endpoints = [[-40, 0], [40, 0]];
        
// add circles
  svg.selectAll("circle")
     .data(dataset)
     .enter()
     .append("circle")
     .classed("points", true)
     .attr("cx", d => xScale(d[0]))
     .attr("cy", d => yScale(d[1]))
     .attr("r", "4")
     .attr("fill", circlecolor);
        
// add draggable line
        
  var dragpath = mylinegen(endpoints);
        
  d3.select("svg")
    .append("path")
    .attr("id", "dragline")
    .attr("d", dragpath)
    .attr("stroke", dragcolor)
    .attr("stroke-width", "3");
        
// add draggable endpoints
        
   d3.select("svg")
      .selectAll("circle.endpoint")
      .data(endpoints)
      .enter()
      .append("circle")
      .attr("class", "endpoint")
      .attr("cx", d => xScale(d[0]))
      .attr("cy", d => yScale(d[1]))
      .attr("r", "4")
      .attr("fill", dragcolor)
      .call(d3.drag()
        .on("drag", dragged));
        
function dragged(d) {
  var new_x = xScale.invert(d3.event.x);
		var new_y = yScale.invert(d3.event.y);
    d3.select(this).data([[new_x, new_y]])
       .attr("cx", d => xScale(d[0]))
       .attr("cy", d => yScale(d[1]));

  var enddata = d3.selectAll("circle.endpoint").data();

  var dragpath = mylinegen(enddata);
  d3.select("path#dragline").attr("d", dragpath); 
};
        
  var bestfit = function() {
        
// get data from circles
  var data = d3.selectAll("circle.points").data();	      
			  
// calculate slope and intercept 
  x = data.map(d => d[0]);
  y = data.map(d => d[1]);	
  Sxx = d3.sum(x.map(d => Math.pow(d-d3.mean(x), 2)));
  Sxy = d3.sum(x.map( (d, i) => (x[i]-d3.mean(x))*(y[i]-d3.mean(y))));
  b1 = Sxy/Sxx;
  b0 = d3.mean(y) - d3.mean(x)*b1;
        
// calculate two points of line for plotting
  var y1 = b0 + b1*xmin;
  var y2 = b0 + b1*xmax;
        
  var mypath = mylinegen([[xmin, y1], [xmax, y2]]);
        
// add best fitting line
  d3.select("svg")
    .append("path")
    .attr("d", mypath)
    .attr("stroke", bestlinecolor)
    .attr("stroke-width", "3");
        
// add equation of the line
  d3.select("h3#bestline")
    .text(`y = ${b1.toFixed(2)}x + ${b0.toFixed(2)}`);
    };

</script>
