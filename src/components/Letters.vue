<template>
  <h1 class="hangman-title">The Hangman</h1>
  <div class="letter-word">It's a {{wordnumber}} letter word</div>
  <div class="letters-box">
    <div variant="primary" size="sm" class="letters" v-for="item in letters" v-bind:key="item.index">{{item}}</div>
  </div> 

</template>

<script>
export default {
  name: 'Letters-json',
  props: {
    letters: String,
    wordnumber: Number
  }
}
</script>

<style>
button {
  font-family: Consolas, 'Courier New', Courier, monospace;
  margin-left: 4px; 
  pointer-events: none;
}

.hangman-title {
  margin-bottom: 80px;
  text-align: left;
}

.letters-box {
  display: flex;
  margin-bottom: 20px;
}

.letter-word {
  margin-bottom: 10px;
  text-align: left;
}

.letters {
  width: 39px;
  height: 39px;
  margin: 5px;
  padding: 5px;
  border: 3px solid #000;
}
</style>