<template>
  <main>
    <h1>Lingo Bingo</h1>
    <h2>Front-End Foxes Edition</h2>
    <h3>(credit to https://github.com/postmodernistx/lingobingo)</h3>
    <p>Click/space to select a tile</p>
    <div class="board">
      <CellButton :word="item" v-for="(item, index) in words" :key="`word-${index}`" />
    </div>
  </main>
</template>

<script>
import CellButton from '@/components/Cell.vue';

export default {
  name: 'App',
  components: { CellButton },
  data() {
    return {
      words: ['Zoomed in 2022', 'Forked a repo in GitHub', 'Made a Sketchnote', 'Submitted a PR', 'Is interested in mentoring future cohort',
        'Heard a good tech talk', 'Had really good food out', 'Slacked with my Mentor', 'Used the DevTools debugger', 'Found a good tech resource',
        'Rode on an airplane recently', 'Loves confetti', 'Has a GitHub account', 'Logged into GitHub', 'Downloaded VS Code',
        'Is proud of their portfolio', 'Found something new in Dev Tools', 'Opened my Browser Console', 'Understands accessibility better', 'Downloaded a VSCode Extension',
        'Saw a concert', 'Has seen a fox in nature', 'Found a bug while in class', 'Googled a topic from class', 'Stayed up late coding',
      ],
    };
  },
  methods: {
    shuffle(array) {
      let currentIndex = array.length;
      let randomIndex;

      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        // eslint-disable-next-line no-plusplus
        currentIndex--;

        // And swap it with the current element.
        // eslint-disable-next-line no-param-reassign
        [array[currentIndex], array[randomIndex]] = [
          array[randomIndex], array[currentIndex]];
      }

      return array;
    },
  },
  mounted() {
    this.words = this.shuffle(this.words);
  },
};
</script>

<style lang="scss">
* { box-sizing: border-box }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  font-family: 'Rock 3D', cursive;
  font-size: 8rem;
  margin: 0;
  line-height: 1.2;
  background-image: linear-gradient(to left,
      #deeb34,
      #ebd634,
      #eb9c34,
      #eb6534,
      #eb3734,
      #eb345f,
      #eb34df
  );
  -webkit-background-clip: text;
  color: transparent;
}
h2 {
  font-family: Roboto,Helvetica Neue,Arial,sans-serif;
  font-size: 4rem;
  margin: 0;
  line-height: 1.2;
  background-image: linear-gradient(to left,
      #deeb34,
      #ebd634,
      #eb9c34,
      #eb6534,
      #eb3734,
      #eb345f,
      #eb34df
  );
  -webkit-background-clip: text;
  color: transparent;
}
.board {
  margin: 30px auto;
  border: 3px solid black;
  padding: 15px;
  border-radius: 5px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  gap: 20px;
  width: 140 * 5px;
}
</style>
