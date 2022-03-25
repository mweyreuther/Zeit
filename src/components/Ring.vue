<template>
  <g transform="translate(50 50)">
    <g ref="group">
      <circle
        clip-path="circle()"
        :r="radius"
        :stroke-width="stroke * 2"
        class="fill-transparent stroke-yellow-200"
      />
      <text
        v-for="(digit, i) in digits"
        class="fill-yellow-200"
        :transform="textTransform(i, digits, radius - size + 0.1)"
        text-anchor="middle"
        alignment-baseline="middle"
        :font-size="size"
      >
        {{ ('0' + i).slice(-2) }}
      </text>
    </g>
  </g>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';

export default {
  name: 'Ring',
  props: {
    digits: {
      type: Number,
      default: 0,
    },
    radius: {
      type: Number,
      default: 0,
    },
    active: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      size: 2,
      stroke: 0.25,
    };
  },
  watch: {
    active: {
      handler(now, before) {
        this.animate(now, before);
      },
      immediate: true,
    },
  },
  methods: {
    textTransform(i, total, r) {
      const tick = (2 * Math.PI) / total;
      const x = -Math.cos(i * tick) * r;
      const y = -Math.sin(i * tick) * r;
      const rotation = (i * 360) / total;
      return `translate(${x} ${y}) rotate(${rotation})`;
    },
    animate(now, before) {
      const tick = !this.digits ? 0 : 360 / this.digits;
      now = 360 - now * tick;
      before = before === undefined ? 0 : 360 - before * tick;
      console.log('now', now, 'before', before);
      anime({
        targets: this?.$refs?.group,
        rotate: [before, now === 360 ? 0 : now],
        easing: 'linear',
        duration: 800,
      });
    },
  },
};
</script>
