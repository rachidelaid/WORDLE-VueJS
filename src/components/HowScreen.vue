<template>
  <div class="how-to">
    <svg @click="goHome" style="width: 24px; height: 24px" viewBox="0 0 24 24">
      <path
        fill="currentColor"
        d="M10,20V14H14V20H19V12H22L12,3L2,12H5V20H10Z"
      />
    </svg>
    <h1>1</h1>
    <h2>Enter the first word</h2>
    <p>
      To get started, simply enter any five-letter word to find out which
      letters match the hidden word. In total, you will have 5 tries to guess
      the hidden word.
    </p>
    <img src="../assets/first.png" />
    <h1>2</h1>
    <h2>Find out what letters are in the hidden word</h2>
    <p>
      If any letters are marked in the accent color, this means that this letter
      is in the hidden word, but doesn't match the exact location in this word.
      If any letter is marked in the darkest color, then it is in that word and
      is in the exact location. If the letters are marked in the light color,
      then it isn't in the hidden word.
    </p>
    <img src="../assets/second.png" />
    <h1>3</h1>
    <h2>Try to guess the hidden word</h2>
    <p>
      Now if you know a few letters with the exact location (darkest color) and
      a few letters that are in the word (accent color) you can try to solve the
      hidden word and win the game!
    </p>
    <img src="../assets/last.png" />
  </div>
</template>

<script>
export default {
  name: 'HowScreen',
  props: ['toggle'],
  setup(props) {
    const goHome = () => {
      props.toggle('start');
    };
    return { goHome };
  },
};
</script>

<style scoped>
.how-to {
  background-color: var(--light-bg);
  padding: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  text-align: center;
}

img {
  margin-bottom: 2rem;
}

svg {
  position: fixed;
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
</style>
