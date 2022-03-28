<template>
  <div class="iphone">
    <Zeit :on="isOn" />
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
    <Switch class="absolute bottom-8 left-8" @on="onOff" />
  </div>
</template>

<script>
import Zeit from './components/Zeit.vue';
import Switch from './components/Switch.vue';
export default {
  name: 'App',
  components: { Zeit, Switch },
  data() {
    return {
      isOn: true,
    };
  },
  mounted() {
    if (this.iOS)
      document.getElementById('app').style.maxHeight = '-webkit-fill-available';
  },
  methods: {
    onOff(isOn) {
      this.isOn = isOn;
    },
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
:root {
  --iPhoneColor: #64748b;
}

body {
  background: #d1d5db; /* bg-gray-300 */
}

#app {
  height: 100%;
  min-height: 100vh;
  display: grid;
  place-items: center;
}
.iphone {
  /* https://codepen.io/adielhercules/pen/dJJGBQ */
  font-family: 'Prompt';
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
  body {
    background: #93c5fd; /* bg-blue-300 */
  }
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
