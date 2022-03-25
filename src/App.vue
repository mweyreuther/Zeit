<template>
  <div id="app" class="bg-gray-500 h-screen p-10">
    <div class="iphone-x bg-green-200">Hello World</div>
    <!-- <svg
      xmlns="http://www.w3.org/2000/svg"
      version="1.1"
      width="100%"
      viewBox="0 0 100 100"
    >
      <g id="hours" transform="translate(50 50)">
        <circle
          cx="0"
          cy="0"
          r="49"
          stroke-width="1"
          class="fill-blue-400 stroke-yellow-200"
        />
        <text
          v-for="(digit, i) in hours"
          class="fill-yellow-200"
          :transform="transform(i, hours.length, 45, 18)"
          text-anchor="middle"
          alignment-baseline="middle"
          :font-size="size"
        >
          {{ digit }}
        </text>
      </g>

      <g id="minutes" transform="translate(50 50)">
        <circle
          cx="0"
          cy="0"
          r="41"
          stroke-width="1"
          class="fill-blue-400 stroke-yellow-200"
        />
        <text
          v-for="(digit, i) in minutes"
          class="fill-yellow-200"
          :transform="transform(i, minutes.length, 37, 45)"
          text-anchor="middle"
          alignment-baseline="middle"
          :font-size="size"
        >
          {{ digit }}
        </text>
      </g>

      <g id="seconds" transform="translate(50 50)">
        <circle
          cx="0"
          cy="0"
          r="33"
          stroke-width="1"
          class="fill-blue-400 stroke-yellow-200"
        />
        <text
          v-for="(digit, i) in minutes"
          class="fill-yellow-200"
          :transform="transform(i, minutes.length, 29, 45)"
          text-anchor="middle"
          alignment-baseline="middle"
          :font-size="size"
        >
          {{ digit }}
        </text>
      </g>
    </svg> -->
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
      size: 3.0,
    };
  },
  mounted() {
    this.hours = Array.from({ length: 24 }, (_, i) => ('0' + i).slice(-2));
    this.minutes = Array.from({ length: 60 }, (_, i) => ('0' + i).slice(-2));
    this.seconds = Array.from({ length: 60 }, (_, i) => ('0' + i).slice(-2));
    console.log(this.minutes);
  },
  methods: {
    transform(i, total, r, offset) {
      const tick = (2 * Math.PI) / total;
      const x = Math.sin(i * tick + offset * tick) * r;
      const y = -Math.cos(i * tick + offset * tick) * r;

      const rotation = (i * 360) / total;
      return `translate(${x} ${y}) rotate(${rotation})`;
    },
  },
};
</script>

<style>
/* @font-face {
  font-family: 'Neuropol';
   src: url('./fonts/NEUROPOL.ttf') format('truetype');
  src: url('./fonts/Neuropol.ttf.eot'),
    url('./fonts/Neuropol.ttf.woff') format('woff'),
    url('./fonts/Neuropol.ttf.svg#Neuropol') format('svg'),
    url('./fonts/Neuropol.ttf.eot?#iefix') format('embedded-opentype');
  font-weight: normal;
  font-style: normal;
} */

* {
  font-family: 'Prompt';
}

.iphone-x {
  overflow: hidden;
  position: relative;
  margin: 0 auto;
  width: 360px;
  height: 780px;
  border-radius: 40px;
  box-shadow: 0px 0px 0px 11px #f4f6fc, 0px 0px 0px 13px #f4f6fc,
    0px 0px 0px 20px #f4f6fc;
}

.iphone-x::before,
.iphone-x::after {
  content: '';
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
.iphone-x:before {
  top: 0px;
  width: 56%;
  height: 30px;
  background-color: #f4f6fc;
  border-radius: 0px 0px 40px 40px;
}
.iphone-x:after {
  bottom: 7px;
  width: 140px;
  height: 4px;
  background-color: #f2f2f2;
  border-radius: 10px;
}
</style>
