<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>EDAV5_3</title>
    <script src="https://d3js.org/d3.v6.min.js"></script>
  </head>

  <body>
  <script>
  d3.csv('https://vizhub.com/curran/datasets/temperature-in-san-francisco.csv')
    .then(data => {
      data.forEach(d => {
        d.temperature = +d.temperature;
        d.timestamp = new Date(d.timestamp);
      });
      console.log(data);
    });
  </script>  
    
 </body>
</html> 
