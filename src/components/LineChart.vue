<template>
  <section></section>
</template>

<script>
import * as d3 from "d3";
import { omzetdata } from "../helpers/graphdata.js";
export default {
  name: "LineChart",
  mounted() {
    const margin = { top: 20, right: 20, bottom: 30, left: 50 };
    const width = 960 - margin.left - margin.right;
    const height = 500 - margin.top - margin.bottom;
    const parseTime = d3.timeParse("%d-%m-%Y");
    const x = d3.scaleTime().range([0, width]);
    const y = d3.scaleLinear().range([height, 0]);

    const valueline = d3
      .line()
      .x(function (d) {
        return x(d.periode);
      })
      .y(function (d) {
        return y(d.omzetontwikkeling);
      })
      .curve(d3.curveBasis);

    const svg = d3
      .select("body")
      .append("svg")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

    omzetdata.forEach((d) => {
      d.periode = parseTime(d.periode);
      d.omzetontwikkeling = +d.omzetontwikkeling;
    });

    x.domain(
      d3.extent(omzetdata, (d) => {
        return d.periode;
      })
    );
    y.domain([
      0,
      d3.max(omzetdata, (d) => {
        return d.omzetontwikkeling;
      }),
    ]);

    const line = svg
      .append("path")
      .data([omzetdata])
      .attr("class", "line")
      .attr("d", valueline);

    const totalLength = line.node().getTotalLength();

    line
      .attr("stroke-dasharray", totalLength)
      .attr("stroke-dashoffset", totalLength)
      .transition()
      .duration(4000)
      .attr("stroke-dashoffset", 0);

    svg
      .append("g")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x));

    svg.append("g").call(d3.axisLeft(y));
  },
};
</script>

<style>
.line {
  fill: none;
  stroke: #454751;
  stroke-width: 2px;
}

text {
  font-family: "Mont Light";
}

path {
  color: grey;
}
</style>