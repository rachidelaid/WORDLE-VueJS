<template>
  <div class="start">
    <div class="wrapper">
      <div class="title">
        <h1>WORDLE</h1>
        <h2>by rachidelaid</h2>
      </div>
    </div>
    <div class="wrapper">
      <div class="actions">
        <button @click="handleClick"><span>></span> Play</button>
        <button @click="handleClick"><span>></span> Settings</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  setup() {
    const handleClick = (e) => {
      document
        .querySelectorAll('.active')
        .forEach((btn) => btn.classList.remove('active'));
      e.target.classList.add('active');
    };

    return { handleClick };
  },
};
</script>

<style scoped>
.start {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  background-color: var(--dark-bg);
}

.wrapper {
  border: 5px solid var(--light-bg);
}

.actions,
.title {
  background-color: var(--light-bg);
  border: 5px solid var(--bg);
  padding: 1rem;
  text-align: center;
  position: relative;
}

.title h1 {
  letter-spacing: 0.5rem;
}

.title h2 {
  color: var(--bg);
}

.actions {
  display: flex;
  padding: 0.4rem 1rem 0.3rem 1rem;
  gap: 1rem;
}

.actions button {
  background: transparent;
  border: none;
  font-family: inherit;
  font-size: 1.58rem;
  color: inherit;
  border-bottom: 3px solid transparent;
  cursor: pointer;
  font-weight: bold;
}

.actions button span {
  visibility: hidden;
}

.actions button.active {
  border-color: var(--dark-bg);
}

.actions button.active span {
  visibility: visible;
}
</style>
