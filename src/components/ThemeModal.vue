<template>
  <svg
    style="width: 24px; height: 24px"
    viewBox="0 0 24 24"
    @click="showModal = true"
  >
    <path
      fill="currentColor"
      d="M17.5,12A1.5,1.5 0 0,1 16,10.5A1.5,1.5 0 0,1 17.5,9A1.5,1.5 0 0,1 19,10.5A1.5,1.5 0 0,1 17.5,12M14.5,8A1.5,1.5 0 0,1 13,6.5A1.5,1.5 0 0,1 14.5,5A1.5,1.5 0 0,1 16,6.5A1.5,1.5 0 0,1 14.5,8M9.5,8A1.5,1.5 0 0,1 8,6.5A1.5,1.5 0 0,1 9.5,5A1.5,1.5 0 0,1 11,6.5A1.5,1.5 0 0,1 9.5,8M6.5,12A1.5,1.5 0 0,1 5,10.5A1.5,1.5 0 0,1 6.5,9A1.5,1.5 0 0,1 8,10.5A1.5,1.5 0 0,1 6.5,12M12,3A9,9 0 0,0 3,12A9,9 0 0,0 12,21A1.5,1.5 0 0,0 13.5,19.5C13.5,19.11 13.35,18.76 13.11,18.5C12.88,18.23 12.73,17.88 12.73,17.5A1.5,1.5 0 0,1 14.23,16H16A5,5 0 0,0 21,11C21,6.58 16.97,3 12,3Z"
    />
  </svg>
  <div class="modal-wrapper" v-if="showModal">
    <div class="modal">
      <svg
        style="width: 24px; height: 24px"
        viewBox="0 0 24 24"
        @click="showModal = false"
      >
        <path
          fill="currentColor"
          d="M12,2C17.53,2 22,6.47 22,12C22,17.53 17.53,22 12,22C6.47,22 2,17.53 2,12C2,6.47 6.47,2 12,2M15.59,7L12,10.59L8.41,7L7,8.41L10.59,12L7,15.59L8.41,17L12,13.41L15.59,17L17,15.59L13.41,12L17,8.41L15.59,7Z"
        />
      </svg>
      <h2>Choose Theme:</h2>
      <div
        v-for="(theme, index) in themes"
        :key="index"
        :id="index"
        :class="`${index === +selectedIndex ? 'active group' : 'group'}`"
        @click="() => selectTheme(index)"
      >
        <div class="color">
          <span :style="`background-color:${theme.bg}`"></span> background color
        </div>
        <div class="color">
          <span :style="`background-color:${theme.light}`"></span> light color
        </div>
        <div class="color">
          <span :style="`background-color:${theme.dark}`"></span> dark color
        </div>
        <div class="color">
          <span :style="`background-color:${theme.accent}`"></span> accent color
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity';
export default {
  name: 'ThemeModal',
  setup() {
    const showModal = ref(false);

    const selectedIndex = ref(
      JSON.parse(localStorage.getItem('themeIndex')) || '0',
    );

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

    const selectTheme = (id) => {
      selectedIndex.value = id;
      localStorage.setItem('themeIndex', id);
      document.documentElement.style.setProperty('--bg', themes[+id].bg);
      document.documentElement.style.setProperty(
        '--accent-color',
        themes[+id].accent,
      );
      document.documentElement.style.setProperty('--dark-bg', themes[+id].dark);
      document.documentElement.style.setProperty(
        '--light-bg',
        themes[+id].light,
      );
    };

    return { themes, selectedIndex, showModal, selectTheme };
  },
};
</script>

<style scoped>
svg {
  position: absolute;
  right: 0.5rem;
  top: 0.5rem;
  color: var(--dark-bg);
  cursor: pointer;
  transition: 0.2s all ease-in-out;
}

svg:hover {
  color: var(--accent-color);
  transform: scale(1.1);
}

.modal-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.6);
}

.modal {
  width: 70%;
  padding: 2rem;
  background-color: var(--bg);
  position: relative;
  display: flex;
  flex-direction: column;
  text-align: center;
  gap: 1rem;
  max-height: 85vh;
  overflow: auto;
}

.group {
  padding: 1rem;
  background-color: var(--light-bg);
}

.group.active {
  border: 2px solid green;
}

.color {
  display: flex;
  gap: 0.5rem;
}

.color:not(:last-child) {
  margin-bottom: 0.5rem;
}

.color span {
  display: block;
  width: 2rem;
  height: 2rem;
  border: 1px solid #fff;
}
</style>
