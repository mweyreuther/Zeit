<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
    height="300%"
    viewBox="0 0 100 100"
    style="transform: translate(3%, -37%)"
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
  data() {
    return { h: 0, m: 0, s: 0 };
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

  mounted() {
    const vm = this;
    setInterval(() => {
      const d = new Date();
      vm.h = d.getHours();
      vm.m = d.getMinutes();
      vm.s = d.getSeconds();
      // console.log(d);
    }, 1000);
  },
  methods: {},
};
</script>
