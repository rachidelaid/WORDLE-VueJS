<template>
  <Start />
</template>

<script>
import Start from './components/Start.vue';

export default {
  name: 'App',
  components: {
    Start,
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

:root {
  --bg: #8b966e;
  --dark-bg: #1f1f1f;
  --light-bg: #c4d0a3;
}

#app {
  font-family: 'VT323', monospace;
  font-size: 130%;
  color: var(--dark-bg);
}
</style>
