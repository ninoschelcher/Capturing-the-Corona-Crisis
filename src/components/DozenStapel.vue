<template>
  <div>
    <p><img src="../../public/assets/stapel_pakketjes.V.1.png" alt="" /></p>
  </div>
</template>

<script>
import * as d3 from "d3";
export default {
  name: "DozenStapel",
};
// create svg element
const svg = d3
  .select("div")
  .append("svg")
  .attr("width", 200)
  .attr("height", 500000);

// Create the scale
const yScale = d3.scaleLinear().domain([1700000, 0]).range([500000, 0]);
const yAxis = d3.axisRight(yScale).ticks(136);

const g = svg
  .append("g")
  .style("class", "axis")
  .style("font-size", "30px")
  .attr("transform", "translate(11,60)")
  .call(yAxis);

g.selectAll("text").attr("transform", "translate(10,0)");
</script>

<style scoped>
p {
  text-align: right;
}
p img {
  max-width: 80%;
  margin-right: 0;
}
svg {
}
</style>
