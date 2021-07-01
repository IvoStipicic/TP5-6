<template>
  <div id="app">

    <Header :color="pickedColor" :winColor="winColor" />

    <Navigator :message="messageDisplay" @restart="restart($event)" :restartMessage="restartMessage" />
    
    <div id="container">
      <div v-for="(square, i) in colors" :key="i">
        <Square :color="colors[i]" @onSquareSelected="onClickSquare($event)" />
      </div>
    </div>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Navigator from './components/Navigator.vue'
import Square from './components/Square.vue'

export default {
  name: 'App',
  components: {
    Header,
    Navigator,
    Square
  },
  mounted () {
    this.restart(6);
  },
  data() {
    return {
      colors: [],
      pickedColor: '',
      messageDisplay: '',
      winColor: '',
      restartMessage: 'new colors'
    }
  },
  methods: {
    onClickSquare(squareColor) {
      if(squareColor === this.pickedColor) {
        this.messageDisplay = "You Picked Right";
        this.setAllColorsTo(squareColor);
        this.winColor = squareColor;
        this.restartMessage = 'Play Again!'
      } else {
        this.messageDisplay = "Try Again!";
      }
    },
    pickColor(quantity) {
      return Math.floor(Math.random() * quantity );
    },
    createRandomStringColor(){
      var newColor = "rgb(" + this.randomInt() + ", " + this.randomInt() + ", " + this.randomInt() + ")" ;
      return newColor;
    },
    randomInt() {
      return Math.floor(Math.random() * 256);
    },
    createNewColors(numbers){
      var arr = [];
      for (var i = 0; i < numbers; i++) {
        arr.push(this.createRandomStringColor());
      }
      return arr;
    },
    setAllColorsTo(color) {
      for (let i = 0; i < this.colors.length; i++) {
        this.colors[i] = color;
      }
    },
    restart(quantity) {
      this.colors = this.createNewColors(quantity);
      this.pickedColor = this.colors[this.pickColor(quantity)];
      this.messageDisplay = '';
      this.winColor = "steelblue";
      this.restartMessage = 'New Colors!'
    },
  }
}
</script>

<style>
  body {
    background: #232323;
    margin: 0;
    font-family: "Montserrat", "Avenir";
  }

  #container {
    margin: 20px auto;
    max-width: 600px;
  }
</style>
