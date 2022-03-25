<template>
  <div id="app" class="bg-gray-500 h-screen">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      version="1.1"
      width="100%"
      viewBox="0 0 100 100"
    >
      <clipPath id="circle">
        <circle cx="0" cy="0" r="50" />
      </clipPath>

      <g id="hours" transform="translate(50 50)">
        <circle
          cx="0"
          cy="0"
          r="50"
          stroke="black"
          stroke-width="4"
          fill="red"
          clip-path="url(#circle)"
        />
        <text
          font-family="Neuropol"
          :x="sin(i, hours.length)"
          :y="cos(i, hours.length)"
          fill="yellow"
          text-anchor="middle"
          alignment-baseline="middle"
          font-size="9"
          v-for="(digit, i) in hours"
        >
          {{ digit }}
        </text>
      </g>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      hours: [],
      minutes: [],
      seconds: [],
    };
  },
  mounted() {
    this.hours = Array.from({ length: 24 }, (_, i) => ('0' + i).slice(-2));
    this.minutes = Array.from({ length: 60 }, (_, i) => i + 1);
    this.seconds = Array.from({ length: 60 }, (_, i) => i + 1);
    console.log(this.minutes);
  },
  methods: {
    sin(i, total) {
      const r = 45;
      const tick = (2 * Math.PI) / total;
      return Math.sin(i * tick + 18 * tick) * r;
    },
    cos(i, total) {
      const r = 45;
      const tick = (2 * Math.PI) / total;
      return -Math.cos(i * tick + 18 * tick) * r;
    },
  },
};
</script>

<style>
@font-face {
  font-family: 'Neuropol';
  src: local('Neuropol'), url('./fonts/Neuropol.ttf.woff') format('woff'),
    url('./fonts/Neuropol.ttf.svg#Neuropol') format('svg'),
    url('./fonts/Neuropol.ttf.eot'),
    url('./fonts/Neuropol.ttf.eot?#iefix') format('embedded-opentype');
  font-weight: normal;
  font-style: normal;
}
/* @font-face {
  font-family: "Merienda";
  src: local("Merienda"),
   url(./fonts/Merienda/Merienda-Regular.ttf) format("truetype");
} */
</style>
