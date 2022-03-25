<template>
  <div class="iphone bg-blue-300">
    <Zeit />
    <div
      class="absolute w-full bg-gradient-to-b from-blue-300/80 to-blue-300/10"
      style="transform: translate(0%, 0%); top: 0; bottom: 500px"
    ></div>
    <div
      class="absolute w-full bg-gradient-to-b from-blue-300/10 to-blue-300/80"
      style="transform: translate(0%, 0%); top: 320px; bottom: 0"
    ></div>
  </div>
</template>

<script>
import Zeit from './components/Zeit.vue';
export default {
  name: 'App',
  components: { Zeit },
};
</script>

<style>
:root {
  --iPhoneColor: #64748b;
}
.iphone {
  /* https://codepen.io/adielhercules/pen/dJJGBQ */
  overflow: clip;
  position: relative;
  margin: 0px auto;
  width: 360px;
  height: 780px;
  border-radius: 40px;
  box-shadow: 0px 0px 0px 20px var(--iPhoneColor);
  font-family: 'Prompt';
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
  bottom: 7px;
  width: 140px;
  height: 4px;
  background-color: #f2f2f2;
  border-radius: 10px;
}
</style>
