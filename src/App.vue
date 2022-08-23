<template>
  <div id="game">
    <b-card header="Game" border-variant="primary" bg-variant="light" header-bg-variant="primary"
        header-text-variant="white">

        <div class="container">
          <div class="row">
            <div class="col-lg-5">
              <div id="gameComponent">
                <StickMan :fails="fails"/>
              </div>
            </div>

            <div class="col-lg-7">
              <div id="gameComponent">
                <Letters :letters="guessedWord" :wordnumber="secretWord.length"/>
              </div>
              
              <div id="gameComponent">
                <Keyboard v-on:key="processLetter" v-on:restart="restart" :usedLetters="usedLetters"/>
              </div>
            </div>
          </div>
        </div>
     

    </b-card>


    <br/>
 </div>
</template>

<script>
import Keyboard from '@/components/Keyboard.vue'
import StickMan from '@/components/StickMan.vue'
import Letters from '@/components/Letters.vue'
import json from '@/words.json';

export default {
  name: 'game-board',
  components: {
    StickMan,
    Letters,
    Keyboard
  },
  data() { 
    return {
      fails: 0,
      guessedWord: "",
      secretWord: "",
      foundLetters: "",
      usedLetters: "", 
      words: json.words
    } 
  },
  mounted: function() {
    window.addEventListener('keyup', this.keyPressed);
    this.restart();
  },
  methods: {
    restart: function() {
      let min = 0;
      let max = this.words.length-1;
      let index = parseInt(Math.random() * (max - min) + min);
      this.secretWord = this.words[index].toUpperCase();
      this.guessedWord = "";
      this.foundLetters = "";
      this.usedLetters = "";
      this.fails = 0;  
      this.guessedWord = this.secretWord.split('').map(() => ' ').join("");
     },
    endgame: function() {
      this.guessedWord = this.secretWord;
     },
    keyPressed(e) {
      let key = e.key.toUpperCase();
      this.processLetter(key);
    },
    processLetter(letter) {
      if (this.fails >= 0 && this.fails < 8 && !this.usedLetters.includes(letter)) {
        if (this.secretWord.includes(letter) 
            && !this.foundLetters.includes(letter)) {
          this.foundLetters += letter;
          this.guessedWord = 
            this.secretWord.split('')
              .map(l => this.foundLetters.includes(l) ? l : ' ').join("");
          if (this.guessedWord == this.secretWord) {
            this.fails = -1;
          }
        } else {
          this.fails++;
          if (this.fails == 8) {
            this.guessedWord = this.secretWord;
          }
        } 
        this.usedLetters += letter;
      } 
      if (letter == "ESCAPE" || letter == " ") {
        this.restart();
      } 
    }
  }
}
</script>

<style>
#game {
  text-align: center;
  margin-top: 10px;
  min-width: 300px;
}
#gameComponent {
  margin-top: 7px;
}
</style>
