<template>
  <section id="boxmountain">
    <div class="scale"></div>
    <div id="boxes">
      <p class="milestone">
        Het aantal mensen dat in de bedrijfstak zorg en welzijn werkt in
        Amsterdam (2020)
      </p>
      <p class="milestone">
        Met een gemiddelde dooshoogte van 80cm en je deze op elkaar stapelt is
        dit net zo hoog als 40 eiffeltorens op elkaar!
      </p>
      <p class="milestone">Denk je dat je er al bijna bent?</p>
      <p class="milestone">
        Het gemiddelde pakket vervoert 50 procent lucht, er zouden dus meer
        pakketjes mee kunnen. Wel zonde eigenlijk..
      </p>
      <p class="milestone">
        Het aantal vastgestelde corona besmettingen was op 1 januari 2021 óók
        800.000
      </p>
      <p class="milestone">
        De 6 nullen zijn inmiddels al bereikt, het is wel een grote stapel zo..
      </p>
      <p class="milestone">
        Zoveel pakketjes moest PostNL nog verwerken per dag begin december.
      </p>
      <p class="milestone">
        Als je de gemiddelde lengte van een doos karton neemt (24cm) en deze
        achter elkaar legt kom je van Utrecht naar Bremen met dit aantal dozen.
      </p>
      <p class="milestone">Het einde is bijna in zicht!</p>
      <p class="milestone">
        Dit aantal staat gelijk aan als 10% van de inwoners in Nederland een
        pakketje zou bestellen.
      </p>
      <p id="top"><img src="../../public/assets/doosbegin.png" alt="" /></p>
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
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p><img src="../../public/assets/doosdoorloop.png" alt="" /></p>
      <p class="smallscreen">
        <img src="../../public/assets/doosdoorloop.png" alt="" />
      </p>
      <p class="smallscreen">
        <img src="../../public/assets/doosdoorloop.png" alt="" />
      </p>
      <p class="smallscreen">
        <img src="../../public/assets/doosdoorloop.png" alt="" />
      </p>
      <p class="smallscreen">
        <img src="../../public/assets/doosdoorloop.png" alt="" />
      </p>
      <p class="smallscreen">
        <img src="../../public/assets/doosdoorloop.png" alt="" />
      </p>
    </div>
  </section>
  <section id="animation2">
    <div class="video-container2">
      <video>
        <source src="../../public/assets/animatie2.mp4" type="video/mp4" />
      </video>
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
  position: relative;
  overflow-x: hidden;
  margin-top: 400px;
}
#boxmountain #top {
  position: relative;
  right: 40px;
  top: 8px;
}
#boxes {
  margin-left: -100px;
  height: 60160px;
  position: relative;
  overflow: hidden;
}
#boxmountain p {
  text-align: center;
  margin-block-start: 0em;
  margin-block-end: 0em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
}
#boxmountain p img {
  max-width: 80%;
  margin-right: 0;
}

.smallscreen {
  display: none;
}

.milestone {
  position: absolute;
  width: 80vw;
  font-weight: bold;
  font-size: 1.8em;
  max-width: 40%;
  margin: 0 auto;
  text-align: center;
}

.milestone:last-child {
  top: 47000px;
}

#boxes p:first-of-type {
  top: 1770px;
  left: 450px;
}

#boxes p:nth-of-type(2) {
  top: 5300px;
  left: 500px;
}

#boxes p:nth-of-type(3) {
  top: 10610px;
  left: 450px;
}

#boxes p:nth-of-type(4) {
  top: 21170px;
  left: 560px;
}
#boxes p:nth-of-type(5) {
  top: 28230px;
  left: 530px;
}

#boxes p:nth-of-type(6) {
  top: 35300px;
  left: 500px;
}

#boxes p:nth-of-type(7) {
  top: 42370px;
  left: 500px;
}
#boxes p:nth-of-type(8) {
  top: 49400px;
  left: 510px;
}
#boxes p:nth-of-type(9) {
  top: 52970px;
  left: 510px;
}
#boxes p:nth-of-type(10) {
  top: 60000px;
  left: 610px;
}

#animation2 {
  position: relative;
  height: 1072px;
}

.video-container2 {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  opacity: 1;
  z-index: 9999;
}
.video-container2 video {
  min-width: 100%;
  min-height: 100%;
  width: 100% !important;
  height: auto !important;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

@media only screen and (max-width: 1440px) {
  p img {
    max-width: 70%;
  }

  #animation2 {
    height: 802px;
  }

  #boxmountain #top {
    right: 0px;
  }
  .smallscreen {
    display: block;
  }

  #boxes p:first-of-type {
    left: 380px;
  }

  #boxes p:nth-of-type(2) {
    left: 330px;
  }

  #boxes p:nth-of-type(3) {
    left: 360px;
  }

  #boxes p:nth-of-type(4) {
    left: 420px;
  }
  #boxes p:nth-of-type(5) {
    left: 340px;
  }

  #boxes p:nth-of-type(6) {
    left: 470px;
  }

  #boxes p:nth-of-type(7) {
    left: 380px;
  }
  #boxes p:nth-of-type(8) {
    left: 420px;
  }
  #boxes p:nth-of-type(9) {
    left: 420px;
  }
  #boxes p:nth-of-type(10) {
    left: 380px;
  }
}
</style>
