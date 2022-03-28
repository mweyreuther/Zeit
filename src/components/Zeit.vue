<template>
  <div class="iphone">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      version="1.1"
      width="750%"
      viewBox="0 0 100 100"
      class="absolute top-1/3 fill-yellow-200"
      style="transform: translate(1%, -50%)"
      @mousemove="move"
    >
      <Ring :digits="24" :radius="radii[0]" :active="h" />
      <Ring :digits="60" :radius="radii[1]" :active="m" />
      <Ring :digits="60" :radius="radii[2]" :active="s" />
      <Ring :digits="0" :radius="radii[3]" :active="0" />
    </svg>
    <div
      class="
        __gradient
        top-0
        bottom-2/3
        bg-gradient-to-b
        from-blue-300/80
        to-blue-300/10
      "
    />
    <div
      class="
        __gradient
        top-1/3
        bottom-0
        bg-gradient-to-t
        from-blue-300/80
        to-blue-300/10
      "
    />
    <Switch class="absolute bottom-6 left-6" @on="onOff" />
  </div>
</template>

<script>
import Ring from './Ring.vue';
import Switch from './Switch.vue';

export default {
  name: 'Zeit',
  components: { Ring, Switch },

  data() {
    return { on: true, h: 0, m: 0, s: 0, intervalID: null };
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
    if (this.iOS)
      document.getElementById('app').style.maxHeight = '-webkit-fill-available';
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
    iOS() {
      // https://stackoverflow.com/questions/9038625/detect-if-device-is-ios
      return (
        [
          'iPad Simulator',
          'iPhone Simulator',
          'iPod Simulator',
          'iPad',
          'iPhone',
          'iPod',
        ].includes(navigator.platform) ||
        // iPad on iOS 13 detection
        (navigator.userAgent.includes('Mac') && 'ontouchend' in document)
      );
    },
  },
};
</script>
<style>
.iphone {
  /* https://codepen.io/adielhercules/pen/dJJGBQ */
  overflow: hidden;
  position: relative;
  width: 360px;
  height: 780px;
  border-radius: 40px;
  box-shadow: 0px 0px 0px 20px var(--iPhoneColor);
  margin: 20px;
  background: #93c5fd; /* bg-blue-300 */
}

.iphone::before,
.iphone::after {
  content: '';
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
.iphone:before {
  /* notch */
  top: 0px;
  width: 56%;
  height: 30px;
  background-color: var(--iPhoneColor);
  border-radius: 0px 0px 40px 40px;
  z-index: 10;
}
.iphone:after {
  /* home button indicator */
  /* bottom: 7px;
  width: 140px;
  height: 4px;
  background-color: #f2f2f2;
  border-radius: 10px; */
}
.__gradient {
  position: absolute;
  width: 100%;
}

@media only screen and (max-width: 414px) {
  .iphone {
    width: 100%;
    height: 100%;
    border-radius: 0;
    box-shadow: none;
  }
  .iphone::before,
  .iphone::after {
    content: none;
  }
}
</style>
