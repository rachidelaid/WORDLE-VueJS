<template>
  <StartScreen v-if="condi === 'start'" :toggle="switchScreens" />
  <GameScreen v-if="condi === 'game'" />
  <HowScreen v-if="condi === 'how'" :toggle="switchScreens" />
</template>

<script>
import StartScreen from './components/StartScreen.vue';
import GameScreen from './components/GameScreen.vue';
import HowScreen from './components/HowScreen.vue';
import { ref } from '@vue/reactivity';

export default {
  name: 'App',
  components: {
    StartScreen,
    GameScreen,
    HowScreen,
  },
  setup() {
    const condi = ref('start');

    const switchScreens = (id) => {
      condi.value = id;
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
  --accent-color: #5d6942;
  --dark-bg: #1f1f1f;
  --light-bg: #c4d0a3;
}

#app {
  font-family: 'VT323', monospace;
  font-size: 130%;
  color: var(--dark-bg);
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>
