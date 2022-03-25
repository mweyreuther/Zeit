<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
    height="300%"
    viewBox="0 0 100 100"
    style="transform: translate(3%, -37%)"
    @mousemove="move"
  >
    <Ring :digits="24" :radius="radii[0]" :active="h" />
    <Ring :digits="60" :radius="radii[1]" :active="m" />
    <Ring :digits="60" :radius="radii[2]" :active="s" />
    <Ring :digits="0" :radius="radii[3]" :active="0" />
  </svg>
</template>

<script>
import Ring from './Ring.vue';
export default {
  name: 'Zeit',
  components: { Ring },
  props: {
    on: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return { h: 0, m: 0, s: 0, intervalID: null };
  },

  computed: {
    radii() {
      const delta = 3.5;
      const inner = 35;
      return Array.from(
        { length: 4 },
        (x, i) => (i + 1) * delta + inner
      ).reverse();
    },
  },
  watch: {
    on: {
      handler(now, before) {
        const vm = this;
        if (now) {
          vm.intervalID = setInterval(() => {
            const d = new Date();
            vm.h = d.getHours();
            vm.m = d.getMinutes();
            vm.s = d.getSeconds();
            // console.log(d);
          }, 1000);
        } else {
          clearInterval(vm.intervalID);
        }
      },
      immediate: true,
    },
  },

  methods: {
    down(e) {
      console.log(e);
    },
    move(evt) {
      const pos = evt.currentTarget.getBoundingClientRect();
      console.log({
        x: evt.clientX - pos.left,
        y: evt.clientY - pos.top,
      });
    },
  },
};
</script>
