<template>
  <section id="boxmountain">
    <div class="scale"></div>
    <div id="boxes">
      <p><img src="../../public/assets/stapel_pakketjes.V.1.png" alt="" /></p>
    </div>
  </section>
</template>

<script>
import * as d3 from "d3";
export default {
  name: "DozenStapel",
  mounted() {
    // create svg element
    const svg = d3
      .select("#boxmountain > div")
      .append("svg")
      .attr("width", 200)
      .attr("height", 35200);

    // Create the scale
    const yScale = d3.scaleLinear().domain([1700000, 0]).range([35000, 0]);
    const yAxis = d3.axisRight(yScale).ticks(34);

    const g = svg
      .append("g")
      .style("class", "axis")
      .style("font-size", "30px")
      .attr("transform", "translate(11,60)")
      .call(yAxis);

    g.selectAll("text").attr("transform", "translate(10,0)");
  },
};
</script>

<style scoped>
#boxmountain {
  display: flex;
}
p {
  text-align: right;
}
p img {
  max-width: 100%;
  margin-right: 0;
}
</style>
