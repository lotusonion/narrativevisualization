# Fuel Efficiency
<html>
    <script src="https://d3js.org/d3.v5.min.js"></script>   
    <script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
    <link rel="stylesheet" type="text/css" href="index.css">

    <body>
        <div>
            <hr>
                <h1>
                    A car's performacne in fuel effciency could be afffected by many factors. In this website, we will help you to make your decision of the car/bran that fits you the most using the data obtained in 2017.
                </h1>
                <ul>
                    <li>
                        <a href="#one" class="contents">Looking for a car that performs better in Highways or Cities?</a>
                    </li>
                    <li>
                        <a href="#two" class="contents">Choose you car based on the number of Engin Cyliners.</a>
                    </li>
                    <li>
                        <a href="#three" class="contents">Choose you car not only based on engines, but also take fuel types into consideration!</a>
                    </li>
                </ul>
            <hr>
        </div>
        <a href="#two" class="back">Next</a>
        <h2 id="one">Looking for a car that performs better in Highways or Cities?</h2>
        <p>See performance of major car brands in cities and highways by clicking on the buttons</p>
        <div>
            <button id="highway" onclick="change('AverageHighwayMPG')">Average Highway MPG</button>
            <button id="city" onclick="change('AverageCityMPG')">Average City MPG</button>
        </div>
        <svg id="scene1" width=1000 height=1200>
            <text x="900" y="700">Good gas mileage</text>

            <line x1="0" y1="700" x2="900" y2="700" stroke="black" stroke-dasharray="4" />
        </svg>
        <script>
            var scene1 = d3.select('#scene1')
            var scene2 = d3.select('#scene2')
            var scene3 = d3.select('#scene3')
            var width = 800, height = 800, spacing=120;
     
            const data =await d3.csv("https://flunky.github.io/cars2017.csv");

            var svg = d3.select("plot1").append("svg").attr("width", width).attr("height", height)
                .append("g").attr("transform", "translate("+ spacing/2 +", "+ spacing/2 +")");
            var y=d3.scaleLinear().domain([0, 120]).range([height-spacing,0]);
            var x=d3.scaleLinear().domain([10, 20, 30, 40, 50]).range([1,width-spacing]);
            svg.append("g").call(d3.axisLeft(y));
            svg.append("g").attr("transform","translate(0,"+(height-spacing) +")").call(d3.axisBottom(x));
            svg.attr("class", "center-screen");

            const line = d3.line()
                .x(d => x(+d.time))
                .y(d => y(+d.value))
            svg.selectAll("myLines")
                .data(dataReady)
                .join("path")
                    .attr("d", d => line(d.values))
                    .attr("stroke", d => myColor(d.name))
                    .style("stroke-width", 4)
                    .style("fill", "none")
            
        </script>
    </body>
</html>