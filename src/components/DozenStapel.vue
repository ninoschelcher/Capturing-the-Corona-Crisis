<template>
  <section id="boxmountain">
    <div class="scale"></div>
    <div id="boxes">
      <p><img src="../../public/assets/doosbegin.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
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
      .attr("height", 60100);

    // Create the scale
    const yScale = d3.scaleLinear().domain([1700000, 0]).range([60000, 0]);
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
p:not(:first-of-type) {
  position: relative;
  right: -150px;
  top: -8px;
}
#boxes {
  margin-left: -250px;
}
p {
  text-align: right;
}
p img {
  max-width: 80%;
  margin-right: 0;
}
</style>
