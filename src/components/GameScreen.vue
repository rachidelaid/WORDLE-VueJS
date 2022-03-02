<template>
  <div class="board">
    <div class="board-wrap">
      <small>{{ error }}</small>
      <div v-for="(row, index) in boxes" :key="index" class="row">
        <div
          v-for="(box, i) in row"
          :key="i"
          :id="box"
          :class="`${box ? 'filled' : ''}`"
        >
          {{ box }}
        </div>
      </div>
    </div>
  </div>
  <div class="keys-wrap">
    <div class="keys" @click="handleClick">
      <div
        v-for="key in keys"
        :key="key"
        :id="key"
        :class="`${'<>'.includes(key) ? 'span-two ' : 'btn'}`"
      >
        {{ key }}
      </div>
    </div>
  </div>
</template>

<script>
import { checkWord, getWord } from '@/words';
import { ref } from '@vue/reactivity';
export default {
  name: 'GameScreen',
  setup() {
    const error = ref('');

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

    const submit = () => {
      if (box < 5 || document.querySelector('.shake')) return;

      const rowElm = document.querySelectorAll('.row')[row];

      if (!checkWord(boxes.value[row].join('').toLowerCase())) {
        rowElm.classList.add('shake');
        error.value = 'word not in the list';

        setTimeout(() => {
          rowElm.classList.remove('shake');
          error.value = '';
        }, 3000);
        return;
      }

      boxes.value[row].forEach((box, i) => {
        if (box.toLowerCase() === word[i]) {
          document
            .querySelectorAll(`.keys #${box}`)
            .forEach((div) => (div.className = 'btn correct'));

          rowElm
            .querySelectorAll(`#${box}`)
            .forEach((div) => (div.className = 'correct'));
        } else if (word.includes(box.toLowerCase())) {
          document
            .querySelectorAll(`.keys #${box}:not(.correct)`)
            .forEach((div) => (div.className = 'btn mid'));

          rowElm
            .querySelectorAll(`#${box}:not(.correct)`)
            .forEach((div) => (div.className = 'mid'));
        } else {
          document
            .querySelectorAll(`.keys #${box}:not(.correct):not(.mid)`)
            .forEach((div) => (div.className = 'btn wrong'));

          rowElm
            .querySelectorAll(`#${box}:not(.correct):not(.mid)`)
            .forEach((div) => (div.className = 'wrong'));
        }
      });

      box = 0;
      row++;
    };

    const handlePress = (e) => {
      if (row > 4) return;

      if (e.key === 'Enter') {
        submit();
        return;
      }

      if (e.key === 'Backspace') {
        box--;
        boxes.value[row][box] = '';
        return;
      }

      if (
        !keys.filter((k) => !'<>'.includes(k)).includes(e.key.toUpperCase()) ||
        box >= 5
      )
        return;

      boxes.value[row][box] = e.key.toUpperCase();
      box++;
    };
    document.body.addEventListener('keyup', handlePress);

    const handleClick = (e) => {
      if (row > 4) return;

      if (e.target.innerText === '>') {
        submit();
        return;
      }

      if (e.target.innerText === '<') {
        box--;
        boxes.value[row][box] = '';
        return;
      }

      if (!e.target.className.includes('btn') || box >= 5) return;

      boxes.value[row][box] = e.target.innerText;
      box++;
    };

    return { error, keys, handleClick, boxes };
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
  transition: 0.15s all ease-in-out;
}

.board .row .filled {
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
  gap: 0.2rem;
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

.board .shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
}

.correct,
.wrong,
.mid {
  color: var(--light-bg);
  border: none !important;
}

.correct {
  background-color: var(--dark-bg);
}

.wrong {
  background-color: var(--bg);
}

.mid {
  background-color: var(--accent-color);
}
</style>
