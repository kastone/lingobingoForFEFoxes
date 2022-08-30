<template>
  <main>
    <h1>Lingo Bingo</h1>
    <h2Front-End Foxes Edition</h2>
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
      words: ['Zoomd in 2020', 'Bought something online', 'has made a Sketchnote', 'Danced by myself to fill in blank', 'Sang Karaoke',
        'Is a musician', 'Owns an unconventional pet', 'Rick rolled someone', 'Traded Crypto', 'Replied All Accidentally',
        'Commented on Tweet by someone famous', 'Took a selfie with someone famous', 'Has a GitHub account', 'Logged into Github', 'Downloaded VSCode',
        'Sold something on EBay-or other', 'Created something on DALL-e', 'Opened Browser Console', 'Seen a broken link on a Website', 'Is an artist',
        'Is a student', 'Saw a fox in nature', 'Wants to learn to code', 'Is an athelete', 'Loves to read',
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
  font-family: 'Roboto,Helvetica Neue,Arial,sans-serif;
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
