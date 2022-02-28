<template>
  <div class="board">
    <div class="board-wrap">
      <div class="row">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
      <div class="row">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
      <div class="row">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
      <div class="row">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
      <div class="row">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
  </div>
  <div class="keys-wrap">
    <div class="keys">
      <div
        v-for="key in keys"
        :key="key"
        :class="`${'<>'.includes(key) ? 'span-two' : ''}`"
      >
        {{ key }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameScreen',
  setup() {
    const keys = 'qwert<yuiopasdfghjklzxcvbnm>'.split('');

    return { keys };
  },
};
</script>

<style scoped>
.board {
  width: 100vw;
  height: calc(100vh - 200px);
  background-color: var(--light-bg);
  display: flex;
  justify-content: center;
  align-items: center;
}

.board-wrap {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.board .row {
  display: flex;
  gap: 0.5rem;
}

.board .row div {
  width: 50px;
  height: 50px;
  border: 2px solid var(--bg);
}

.board .row .active {
  border-color: var(--dark-bg);
}

.keys-wrap {
  width: 100vw;
  height: 200px;
  background-color: var(--bg);
  display: flex;
  justify-content: center;
  align-items: center;
}

.keys {
  display: grid;
  grid-template-columns: repeat(8, 35px);
  gap: 0.5rem;
  place-items: center;
}

.keys div {
  width: 100%;
  height: 35px;
  aspect-ratio: 1;
  border: 2px solid var(--light-bg);
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.span-two {
  grid-column: span 3;
}
</style>
