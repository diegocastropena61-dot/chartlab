<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Gráfico de Barras con D3.js</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
  <style>
    .bar {
      fill: steelblue;
    }
    .bar:hover {
      fill: orange;
    }
    .axis-label {
      font-size: 12px;
    }
  </style>
</head>
<body>
  <svg width="600" height="400"></svg>

  <script>
    const data = [25, 30, 45, 60, 20, 65, 75];

    const svg = d3.select("svg");
    const width = +svg.attr("width");
    const height = +svg.attr("height");
    const margin = { top: 20, right: 30, bottom: 30, left: 40 };

    const x = d3.scaleBand()
      .domain(data.map((d, i) => i))
      .range([margin.left, width - margin.right])
      .padding(0.1);

    const y = d3.scaleLinear()
      .domain([0, d3.max(data)])
      .nice()
      .range([height - margin.bottom, margin.top]);

    svg.append("g")
      .attr("fill", "steelblue")
      .selectAll("rect")
      .data(data)
      .join("rect")
        .attr("class", "bar")
        .attr("x", (d, i) => x(i))
        .attr("y", d => y(d))
        .attr("height", d => y(0) - y(d))
        .attr("width", x.bandwidth());

    svg.append("g")
      .attr("transform", `translate(0,${height - margin.bottom})`)
      .call(d3.axisBottom(x).tickFormat(i => `Item ${i + 1}`))
      .selectAll("text")
        .attr("class", "axis-label");

    svg.append("g")
      .attr("transform", `translate(${margin.left},0)`)
      .call(d3.axisLeft(y))
      .selectAll("text")
        .attr("class", "axis-label");
  </script>
</body>
</html>
# chartlab
