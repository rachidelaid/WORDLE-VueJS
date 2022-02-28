<template>
  <StartScreen v-if="condi" :toggle="switchScreens" />
  <GameScreen v-else />
</template>

<script>
import StartScreen from './components/StartScreen.vue';
import GameScreen from './components/GameScreen.vue';
import { ref } from '@vue/reactivity';

export default {
  name: 'App',
  components: {
    StartScreen,
    GameScreen,
  },
  setup() {
    const condi = ref(true);

    const switchScreens = () => {
      condi.value = !condi.value;
    };

    return { condi, switchScreens };
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
