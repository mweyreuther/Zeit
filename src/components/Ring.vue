<template>
  <g :transform="groupTransform">
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
</template>

<script>
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
  computed: {
    groupTransform() {
      if (!this.digits) return `translate(50 50)`;
      const tick = 360 / this.digits;
      return `translate(50 50) rotate(${-this.active * tick})`;
    },
  },
  mounted() {
    // console.log('digits', this.digits);
  },

  methods: {
    textTransform(i, total, r) {
      const tick = (2 * Math.PI) / total;
      const x = -Math.cos(i * tick) * r;
      const y = -Math.sin(i * tick) * r;
      const rotation = (i * 360) / total;
      return `translate(${x} ${y}) rotate(${rotation})`;
    },
  },
};
</script>
