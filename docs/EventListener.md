<html lang="en">
	<head>
		<meta charset="utf-8">
		<title>Six Blue Circles</title>

		<script src="https://d3js.org/d3.v4.min.js"></script>  <!-- link to D3 Version 4 library -->


	</head>

	<body>

		<script>
		  var dataset = [100, 150, 200, 250, 300];
		  var svg = d3.select("body").append("svg")
		    .attr("width", "600").attr("height", "400");
		  svg.append("rect").attr("width", "600")
		    .attr("height", "400").attr("fill", "aliceblue");
		  svg.selectAll("circle")
		    .data(dataset)
		    .enter()
		    .append("circle")
		    .attr("cx", d => d)
		    .attr("cy", d => d)
		    .attr("r", "15")
		    .attr("fill", "purple")
		    .on("click", function () {
		      d = new Date();
		      if (d.getSeconds() % 2 == 0) {
		        d3.select(this).attr("cx", "100");
		        } else {
		        d3.select(this).attr("cx", "150");
		        }
		      });
		</script>

	</body>

</html>
