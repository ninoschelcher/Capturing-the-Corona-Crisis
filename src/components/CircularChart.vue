<template>
  <section></section>
</template>

<script>
import * as d3 from "d3";
import { branchedata } from "../helpers/graphdata.js";
export default {
  name: "CircularChart",
  mounted() {
    //https://gist.github.com/AntonOrlov/6b42d8676943cc933f48a43a7c7e5b6c//
    const margin = { top: 50, right: 20, bottom: 80, left: 50 };
    const width = 960;
    const height = 550;
    const chartRadius = height / 2 - 40;

    let tooltip = d3.select("section").append("div").attr("class", "tooltip");

    const color = [
      "#440154ff",
      "#31668dff",
      "#37b578ff",
      "#fde725ff",
      "#B35900",
    ];

    const svg = d3
      .select("section")
      .append("svg")
      .attr("width", width + margin.top)
      .attr("height", height)
      .append("g")
      .attr("transform", "translate(" + width / 2 + "," + 290 + ")");

    const PI = Math.PI,
      arcMinRadius = 10,
      arcPadding = 10,
      labelPadding = -5,
      numTicks = 10;

    const scale = d3
      .scaleLinear()
      .domain([0, 90])
      .range([0, 1.68 * PI]);

    const ticks = scale.ticks(numTicks).slice(0, -1);
    const keys = branchedata.map((d) => d.branche);
    const numArcs = keys.length;
    const arcWidth =
      (chartRadius - arcMinRadius - numArcs * arcPadding) / numArcs;

    const arc = d3
      .arc()
      .innerRadius((d, i) => getInnerRadius(i))
      .outerRadius((d, i) => getOuterRadius(i))
      .startAngle(0)
      .endAngle((d) => scale(d));

    const radialAxis = svg
      .append("g")
      .attr("class", "r axis")
      .selectAll("g")
      .data(branchedata)
      .enter()
      .append("g");

    radialAxis
      .append("circle")
      .attr("r", (d, i) => getOuterRadius(i) + arcPadding);

    radialAxis
      .append("text")
      .attr("x", labelPadding)
      .attr("y", (d, i) => -getOuterRadius(i) + arcPadding + 10)
      .text((d) => d.branche);

    const axialAxis = svg
      .append("g")
      .attr("class", "a axis")
      .selectAll("g")
      .data(ticks)
      .enter()
      .append("g")
      .attr("transform", (d) => "rotate(" + (rad2deg(scale(d)) - 90) + ")");

    axialAxis.append("line").attr("x2", chartRadius);

    axialAxis
      .append("text")
      .attr("x", chartRadius + 10)
      .style("text-anchor", (d) =>
        scale(d) >= PI && scale(d) < 2 * PI ? "end" : null
      )
      .attr(
        "transform",
        (d) =>
          "rotate(" +
          (90 - rad2deg(scale(d))) +
          "," +
          (chartRadius + 10) +
          ",0)"
      )
      .text((d) => d);

    //data arcs
    const arcs = svg
      .append("g")
      .attr("class", "data")
      .selectAll("path")
      .data(branchedata)
      .enter()
      .append("path")
      .attr("class", "arc")
      .style("fill", (d, i) => color[i])
      .style("cursor", "pointer");

    arcs
      .transition()
      .delay((d, i) => i * 200)
      .duration(1000)
      .attrTween("d", arcTween);

    arcs.on("mousemove", showTooltip);
    arcs.on("mouseout", hideTooltip);

    function arcTween(d, i) {
      let interpolate = d3.interpolate(0, d.stijging);
      return (t) => arc(interpolate(t), i);
    }

    function showTooltip(d, branchedata) {
      tooltip
        .style("left", d.offsetX + "px")
        .style("top", d.offsetY + 10 + "px")
        .style("display", "block")
        .html(
          "Branche: " +
            branchedata.branche +
            "<br>" +
            "Stijging: " +
            branchedata.stijging +
            "&#37;"
        );
    }

    function hideTooltip() {
      tooltip.style("display", "none");
    }

    function rad2deg(angle) {
      return (angle * 180) / PI;
    }

    function getInnerRadius(index) {
      return arcMinRadius + (numArcs - (index + 1)) * (arcWidth + arcPadding);
    }

    function getOuterRadius(index) {
      return getInnerRadius(index) + arcWidth;
    }

    svg
      .append("text")
      .attr("x", 0)
      .attr("y", -255)
      .attr("text-anchor", "middle")
      .style("font-size", "20px")
      .style("font-family", "Mont Heavy")
      .text("Productbranche groei Q3 in 2020");
  },
};
</script>

<style>
svg {
  margin: 0px auto;
  display: block;
}

path.arc {
  opacity: 0.9;
  transition: opacity 0.5s;
}

path.arc:hover {
  opacity: 0.7;
}

.axis line,
.axis circle {
  stroke: #cccccc;
  stroke-width: 1px;
}

.axis circle {
  fill: none;
}

.r.axis text {
  text-anchor: end;
}

.tooltip {
  position: absolute;
  display: none;
  background: rgba(0, 0, 0, 0.6);
  border-radius: 3px;
  box-shadow: -3px 3px 15px #888;
  color: white;
  padding: 6px;
}
</style>