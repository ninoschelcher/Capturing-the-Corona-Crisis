<template>
  <section id="linesection">
    <h2>Omzet stijging webwinkels 2019-2020</h2>
    <p>
      Deze grafiek toont de procentuele omzet van 2019 en 2020 in vergelijking
      met dezelfde periode het jaar ervoor. De stijging begint wanneer Corona
      Nederland had bereikt.
    </p>
    <div id="line"></div>
  </section>
</template>

<script>
import * as d3 from "d3";
import { omzetdata } from "../helpers/graphdata.js";
export default {
  name: "LineChart",
  mounted() {
    const margin = { top: 50, right: 20, bottom: 80, left: 100 };
    const width = 980 - margin.left - margin.right;
    const height = 550 - margin.top - margin.bottom;
    const parseTime = d3.timeParse("%d-%m-%Y");
    const x = d3.scaleTime().range([0, width]);
    const y = d3.scaleLinear().range([height, 0]);

    const tooltip = d3
      .select("div#line")
      .append("div")
      .attr("class", "tooltip");

    const valueline = d3
      .line()
      .x(function (d) {
        return x(d.periode2);
      })
      .y(function (d) {
        return y(d.omzetontwikkeling);
      });

    const svg = d3
      .select("#line")
      .append("svg")
      .attr("class", "linechart")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

    omzetdata.forEach((d) => {
      d.periode2 = parseTime(d.periode);
      d.omzetontwikkeling = +d.omzetontwikkeling;
    });

    x.domain(
      d3.extent(omzetdata, (d) => {
        return d.periode2;
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

    const dots = svg
      .selectAll("circle")
      .data(omzetdata)
      .enter()
      .append("circle")
      .attr("r", 0)
      .attr("cx", function (d) {
        return x(d.periode2);
      })
      .attr("cy", function (d) {
        return y(d.omzetontwikkeling);
      });

    dots
      .style("opacity", 0)
      .transition()
      .duration(4000)
      .delay(function (_, i) {
        return i * 200;
      })
      .style("opacity", 1)
      .style("cursor", "pointer")
      .attr("r", 5);

    dots.on("mousemove", showTooltip);
    dots.on("mouseout", hideTooltip);

    function showTooltip(d, omzetdata) {
      tooltip
        .style("left", d.pageX + "px")
        .style("top", d.pageY + 10 + "px")
        .style("display", "block")
        .html(
          "Datum: " +
            omzetdata.periode +
            "<br>" +
            "Stijging: " +
            omzetdata.omzetontwikkeling +
            "&#37;"
        );
    }

    function hideTooltip() {
      tooltip.style("display", "none");
    }

    svg
      .append("text")
      .attr("class", "linelabels")
      .attr(
        "transform",
        "translate(" + width / 2 + " ," + (height + margin.top + 10) + ")"
      )
      .style("text-anchor", "middle")
      .text("Periode");

    svg
      .append("text")
      .attr("class", "linelabels")
      .attr("transform", "rotate(-90)")
      .attr("y", -85)
      .attr("x", 0 - height / 2)
      .attr("dy", "1em")
      .style("text-anchor", "middle")
      .text("Omzet stijging");
  },
};
</script>

<style>
#linesection {
  text-align: center;
}
#linesection h2 {
  font-size: 2em;
  margin-bottom: 0.5em;
}
#linesection p {
  margin: 0 auto;
  max-width: 40%;
}
.linechart .linelabels {
  font-size: 25px;
}
.linechart text {
  font-size: 15px;
}
.line {
  fill: none;
  stroke: #454751;
  stroke-width: 2px;
}

text {
  font-family: "sofia-pro";
}

path {
  color: grey;
}
</style>