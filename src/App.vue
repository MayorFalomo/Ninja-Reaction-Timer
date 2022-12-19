<template>
  <div class="container">
    <h1>Ninja Reaction Timer</h1>
    <button @click="start" :disabled="isPlaying">Play</button>
    <!-- If isPlaying is true then disable-->
    <Block v-if="isPlaying" :delay="delay" @end="endGame" />
    <!-- This component only runs when isPlaying is true-->
    <!--Sending :delay as props to Block component-->
    <Results v-if="showResults" :score="score">
      <p v-if="high">Rank: Your speed rivals Naruto</p>
      <p v-if="average">Rank: Even Tof in Avatar was faster and she's blind</p>
      <p v-if="low">Rank: What a slow Ninja</p>
    </Results>
  </div>
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";

export default {
  name: "App",
  data() {
    return {
      isPlaying: false, // To disable the button when you click to start the game
      delay: null, // This is for setting the delay of the block
      score: null, // Score starts as null
      showResults: false, // It doesn't show the p tag at first because 'showResults is set to false
      comments: false,
      high: false,
      average: false,
      low: false,
    };
  },
  components: {
    Block,
    Results,
  },
  methods: {
    start() {
      //This function runs when we click the button
      this.delay = 2000 + Math.random() * 5000; // Delay is done randomly between 5s and 2s
      this.isPlaying = true; //The button is disabled when isplaying becomes true
      this.showResults = false; // clears the p tag again since we want to play again
      this.scoring = false;
    },
    endGame(reactionTime) {
      this.score = reactionTime; // We are Assigning the reactionTime we sent from Block component to this.score we defined here
      this.isPlaying = false; // button become enabled again since we want to play again
      this.showResults = true; // showResults becomes true when the game ends so the score shows.
      if (this.score < 300) {
        this.high = true;
      } else if (this.score > 300 && this.score < 800) {
        this.average = true;
      } else if (this.score > 800) {
        this.low = true;
      }
      console.log(this.score, this.low);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
body {
  background-color: rgba(255, 255, 255, 0.303);
}
button {
  background: #0faf87;
  color: white;
  border: none;
  outline: none;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
  padding: 8px 15px;
  font-size: 20px;
  border-radius: 7px;
}
button[disabled] {
  opacity: 0.3;
  cursor: not-allowed;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
p {
  font-size: 20px;
  line-height: 35px;
}
span {
  font-size: 24px;
  font-weight: 900px;
}
</style>
