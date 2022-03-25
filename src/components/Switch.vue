<template>
  <div class="switch">
    <input type="checkbox" id="switch" v-model="checked" />
    <label for="switch" />
  </div>
</template>

<script>
export default {
  name: 'Switch',
  data() {
    return { checked: true };
  },
  watch: {
    checked: {
      handler(now, before) {
        this.$emit('on', now);
      },
      immediate: true,
    },
  },
};
</script>

<style>
:root {
  --color: #fef08a;
}
.switch {
  transform: scale(1);
}

input[type='checkbox'] {
  height: 0;
  width: 0;
  visibility: hidden;
}

label:hover {
  background: #fef08a50;
}
label {
  cursor: pointer;
  /* text-indent: -9999px; */
  width: 50px;
  height: 50px;
  display: grid;
  place-items: center;
  border-radius: 100px;
  border-width: 1px;
  border-color: var(--color);
  box-sizing: content-box;
  position: relative;
  transition: 0.3s;
}

label:after {
  color: var(--color);
  position: absolute;
  display: grid;
  place-items: center;
  top: 4px;
  left: 4px;
  width: 42px;
  height: 42px;
  border-radius: 90px;
  border-width: 0px;
  border-color: var(--color);
  transition: 0.3s;
}

/* input:checked + label {
  background: yellow;
} */

input:checked + label:after {
  /* background: #fef08a; */
  content: 'on';
}
input + label:after {
  /* background: #fef08a; */
  content: 'off';
}
input:checked + label:after {
  left: calc(100% - 4px);
  transform: translateX(-100%);
  transition: 0.3s;
}

label:active:after {
  /* width: 92px; */
}
</style>
