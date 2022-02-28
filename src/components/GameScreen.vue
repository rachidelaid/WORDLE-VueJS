<template>
  <div class="board">
    <div class="board-wrap">
      <div v-for="(row, index) in boxes" :key="index" class="row">
        <div v-for="(box, i) in row" :key="i" :class="`${box ? 'filled' : ''}`">
          {{ box }}
        </div>
      </div>
    </div>
  </div>
  <div class="keys-wrap" @keyup="press">
    <div class="keys" @click="press">
      <div
        v-for="key in keys"
        :key="key"
        :class="`${'<>'.includes(key) ? 'span-two ' : 'btn'}`"
      >
        {{ key }}
      </div>
    </div>
  </div>
</template>

<script>
import { getWord } from '@/words';
import { ref } from '@vue/reactivity';
export default {
  name: 'GameScreen',
  setup() {
    const word = getWord();
    const keys = 'QWERTYUIOPASDFGHJKLZXCVB<NM>'.split('');

    const boxes = ref([
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
      ['', '', '', '', ''],
    ]);

    let box = 0;
    let row = 0;

    console.log(word);

    const press = (e) => {
      if (
        !keys.filter((k) => !'<>'.includes(k)).includes(e.key.toUpperCase()) ||
        // !e.target.className.includes('btn') ||
        box >= 5
      )
        return;

      boxes.value[row][box] = e.key ? e.key.toUpperCase() : e.target.innerText;
      box++;
    };

    document.body.addEventListener('keypress', press);

    return { keys, press, boxes };
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
  text-align: center;
}

.board .row {
  display: flex;
  gap: 0.5rem;
}

.board .row div {
  width: 50px;
  height: 50px;
  border: 2px solid var(--bg);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2.6rem;
  font-weight: bold;
}

.board .row .filled {
  border-color: var(--dark-color);
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
