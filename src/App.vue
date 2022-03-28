<template>
  <div class="flex gap-4" v-if="false">
    <a href="#/">Zeit</a> | <a href="#/icon">Icon</a> |
    <a href="#/non-existent-path">Broken Link</a>
  </div>

  <component :is="currentView" />
</template>

<script>
import Zeit from './components/Zeit.vue';
import Icon from './components/Icon.vue';
import NotFound from './components/NotFound.vue';

const routes = {
  '/': Zeit,
  '/icon': Icon,
};

export default {
  name: 'App',
  components: { Zeit, Icon, NotFound },
  data() {
    return {
      currentPath: window.location.hash,
    };
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound;
    },
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash;
    });
  },
};
</script>

<style>
:root {
  --iPhoneColor: #64748b; /* bg-slate-500 */
  --bg-gray: #d1d5db; /* bg-gray-300 */
  --bg-blue: #93c5fd; /* bg-blue-300 */
  --bg-yellow: #fef08a; /* bg-yellow-200 */
}
body {
  font-family: 'Prompt';
  background: var(--bg-gray);
}
#app {
  height: 100%;
  min-height: 100vh;
  display: grid;
  place-items: center;
}

@media only screen and (max-width: 414px) {
  body {
    background: var(--bg-blue);
  }
}
</style>
