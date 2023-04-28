<template>
  <div id="app">
    <h1 style="text-align: center">Dice Game</h1>
    <div class="wrapper clearfix">
      <players
        v-bind:activePlayer="activePlayer"
        v-bind:scoresPlayer="scoresPlayer"
        v-bind:currentScore="currentScore"
      />
      <controler-vue
        v-bind:isPlaying="isPlaying"
        v-on:handleNewGame="handleNewGame"
        v-on:handleRollDice="handleRollDice"
        v-on:handleHoldScore="handleHoldScore"
        v-bind:finalScore="finalScore"
        v-on:handleChangeFinalScore="handleChangeFinalScore"
      />
      <Dices v-bind:dices="dices" />
      <popup-vue
        v-on:handleConfirm="handleConfirm"
        v-bind:isOpenpopup="isOpenpopup"
      />
    </div>
  </div>
</template>

<script>
import ControlerVue from "./components/Controler.vue";
import Dices from "./components/Dices.vue";
import Players from "./components/Players.vue";
import PopupVue from "./components/Popup.vue";
export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenpopup: false,
      activePlayer: 1,
      dices: [1, 5],
      scoresPlayer: [0, 0],
      currentScore: 50,
      nextPlayer: 0,
      finalScore: 10,
      isWinner: "",
    };
  },

  methods: {
    handleNewGame() {
      this.isPlaying = true;
      this.isOpenpopup = true;
      this.activePlayer = 0;
      this.dices = [1, 1];
      this.scoresPlayer = [0, 0];
      this.currentScore = 0;
    },
    reload(){
      this.isPlaying = false;
      this.activePlayer = 0;
      this.dices = [1, 1];
      this.scoresPlayer = [0, 0];
      this.currentScore = 0;
    },
    handleRollDice() {
      this.dices = [
        Math.floor(Math.random() * 6) + 1,
        Math.floor(Math.random() * 6) + 1,
      ];
      if (this.isPlaying) {
        this.currentScore += this.dices[0] + this.dices[1];
      }
      if (this.activePlayer == 0) {
        if (
          (this.dices[0] === 1 && this.dices[1] !== 1) ||
          (this.dices[0] !== 1 && this.dices[1] === 1)
        ) {
          this.activePlayer = 1;
          this.currentScore = 0;
        }
      } else if (this.activePlayer == 1) {
        if (
          (this.dices[0] === 1 && this.dices[1] !== 1) ||
          (this.dices[0] !== 1 && this.dices[1] === 1)
        ) {
          this.activePlayer = 0;
          this.currentScore = 0;
        }
      }
    },
    handleConfirm() {
      this.isOpenpopup = false;
    },
    handleHoldScore() {
      this.scoresPlayer[this.activePlayer] += this.currentScore;
      this.currentScore = 0;

      let { scoresPlayer, finalScore } = this;
      if (scoresPlayer[0] >= finalScore) {
        alert("nguoi choi 1 thang");
        this.reload()
      } else if (scoresPlayer[1] >= finalScore) {
        alert("nguoi choi 2 thang");
        this.reload()
      }
    },
    handleChangeFinalScore(e) {
      var number = parseInt(e.target.value);
      if (isNaN(number)) {
        this.finalScore = "";
      } else {
        this.finalScore = number;
      }
    },
  },
  computed: {},
  components: {
    Players,
    ControlerVue,
    Dices,
    PopupVue,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("/public/assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
