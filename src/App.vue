<template>
  <main>
    <h1>Lingo Bingo</h1>
    <h2>(credit to https://github.com/postmodernistx/lingobingo)</h2>

    <p :class="{ active: isBingo }">
      {{ !isBingo ? 'Click/space to select a tile' : 'BINGO!' }}
    </p>
    <div class="board">
      <CellButton
        :word="item"
        v-for="(item, index) in words"
        :key="`word-${index}`"
        @click="win(index)"
        :disabled="isBingo"
      />
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
      words: [
        'Lighthouse',
        'Primary color',
        'sans-serif',
        'SEO',
        'graphic profile',
        'secondary color',
        'color wheel',
        'UI/UX',
        'gitmoji',
        'React',
        'Vue',
        'Sass',
        'Illustrator',
        'Photoshop',
        'Figma',
        'pull request',
        'API',
        'a11y',
        'Internet Explorer',
        'WordPress',
        'Heroku',
        'HTML',
        'router',
        'responsive',
        'agile',
      ],
      N: '',
      selectedItems: [],
      isBingo: false,
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
        [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
      }

      return array;
    },

    win(index) {
      const vector = this.selectedItems;

      const n = Math.sqrt(this.N);
      vector[index] = 1;

      let linha = 0;
      let coluna = 0;
      let diagMain = 0;
      let diagSec = 0;

      for (let i = 0; i < this.N; i += n) {
        linha = 0;
        coluna = 0;

        for (let j = 0; j < n; j += 1) {
          const indexLinha = j + i;
          linha += vector[indexLinha];
          const indexColuna = j * n + i / n;
          coluna += vector[indexColuna];
        }

        for (let k = i / n; k < n; k += n) {
          const indexDiagMain = k + i;
          diagMain += vector[indexDiagMain];
        }

        for (let l = i / n + 1; l <= n; l += n) {
          const indexDiagSec = (n - 1) * l;
          diagSec += vector[indexDiagSec];
        }
        if (linha === n || coluna === n || diagMain === n || diagSec === n) {
          break;
        }
      }

      if (linha === n || coluna === n || diagMain === n || diagSec === n) {
        console.log('BINGO');
        this.isBingo = !this.isBingo;
      } else {
        console.log('NO MATCH :(');
      }
      return this.isBingo;
    },
  },
  mounted() {
    this.words = this.shuffle(this.words);
    this.N = this.words.length;
    for (let x = 0; x < this.N; x += 1) {
      this.selectedItems[x] = 0;
    }
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}
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
  background-image: linear-gradient(
    to left,
    #0dc4b7,
    #9a2654,
    #2a47d5,
    #19d519,
    #e9ff00,
    #ff8000,
    #f30a0a
  );
  -webkit-background-clip: text;
  color: transparent;
}

.active {
  font-weight: bolder;
  font-size: xx-large;
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
