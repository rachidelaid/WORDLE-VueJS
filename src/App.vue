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
  mounted() {
    const themes = [
      {
        bg: '#8b966e',
        light: '#c4d0a3',
        dark: '#1f1f1f',
        accent: '#5d6942',
      },
      {
        bg: '#966d8c',
        light: '#d1a3bd',
        dark: '#210317',
        accent: '#773863',
      },
      {
        bg: '#5e7a9e',
        light: '#a3b3d1',
        dark: '#020a21',
        accent: '#0052bf',
      },
      {
        bg: '#9e775d',
        light: '#e2c29c',
        dark: '#211201',
        accent: '#bf6200',
      },
    ];

    const index = JSON.parse(localStorage.getItem('themeIndex')) || '0';

    document.documentElement.style.setProperty('--bg', themes[+index].bg);
    document.documentElement.style.setProperty(
      '--accent-color',
      themes[+index].accent,
    );
    document.documentElement.style.setProperty(
      '--dark-bg',
      themes[+index].dark,
    );
    document.documentElement.style.setProperty(
      '--light-bg',
      themes[+index].light,
    );
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

* {
  scrollbar-color: var(--light-bg) var(--accent-color);
}
</style>
