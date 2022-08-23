<template>
  <div id="buttons" class="button">
    <div class="text-play">Play with word</div>
    <div class="button__letters-box" v-for="row in keys" :key="row">
      <b-button class="button__letters" v-for="key in row" 
                :key="key" 
                size="sm" 
                pill 
                :disabled="usedLetters.includes(key)"
                v-on:click="click(key, $event)"
                >
                {{key}}
      </b-button>
    </div>
    <div class="buttons__control">
      <div id="endgame">
        <b-button class="buttons__endgame" v-on:click="endGame">End Game</b-button>
      </div>
      <div id="restart">
        <b-button class="buttons__restart" v-on:click="restart">Start new game</b-button>
      </div>
    </div>
  </div> 
</template>

<script>
export default {
  name: 'Keyboard-letters',
  props: {
    usedLetters: String
  },
  data() { 
    return {
      keys : ["ABCDEFGHIJKLMNOPQRSTUVWXYZ"],
    } 
  },
  methods: {
    click(key,e) {
      this.$parent.processLetter(key);
      e.target.blur();
    },
    restart(e) { 
      this.$emit('restart');
      e.target.blur();
    },
    endGame(e) {
      this.$parent.endgame();
      e.target.blur();
    }
  }
}
</script>

<style scoped>
button {
  font-family: 'Courier New', Courier, monospace;
  font-weight: bold;
  margin-left: 2px;
  margin-top: 3px;
}

.text-play {
  text-align: left;
}

.button__letters-box {
  display: flex;
  flex-wrap: wrap;
  max-width: 450px;
}

.buttons__control {
  display: flex;
  align-content: center;
  margin-top: 60px;
}

.buttons__endgame,
.buttons__restart {
  padding: 3px 40px;
  box-shadow: 0px 0px 4px 2px rgba(115,115,115,0.8);
  cursor: pointer;
  text-transform: uppercase;
}

.buttons__endgame {
  margin-right: 20px;
}

.button .button__letters {
  display: inline-block;
  width: 35px;
  margin: 5px;
  padding: 5px;
  font-weight: 700;
  box-shadow: 0px 0px 4px 2px rgba(115,115,115,0.8);
  cursor: pointer;
}

.button__letters[disabled="true"] {
  opacity: .5;
  box-shadow: none;
}

</style>