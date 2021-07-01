<template>

  <section class="src-components-navigator">
    <div id="navigator">
      <button id="reset" @click="onDifficultySelect(difficulty)">{{ restartMessage }}</button>
      <span id="message" ref="message"> {{ message }} </span>

      <button :class="{ selected: isEasySelected }" @click="onDifficultySelect(3)">easy</button>
      <button :class="{ selected: isHardSelected }" @click="onDifficultySelect(6)">hard</button>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-navigator',
    props: ['message', 'restartMessage'],
    mounted () {

    },
    updated () {
      if(this.message === "Try Again!") {
        this.$refs.message.style.color = "#000000"
      }
    },
    data () {
      return {
        isEasySelected: false,
        isHardSelected: true,
        difficulty: 6,
      }
    },
    methods: {
      onDifficultySelect(difficulty) {
        this.$emit('restart', difficulty);
        if(difficulty === 6) {
          this.isHardSelected = true;
          this.isEasySelected = false;
          this.difficulty = 6;
        } else {
          this.isHardSelected = false;
          this.isEasySelected = true;
          this.difficulty = 3;
        }
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">

  #navigator {
    background: #ffffff;
    height: 30px;
    text-align: center;
    margin: 0;
    margin-top: -30px;
  }

  #message {
    color: #ffffff;
    display: inline-block;
    width: 20%;
  }

  .selected {
    background-color: steelblue;
    color: white;
  }

  button {
    border: none;
    background-color: white;
    font-family: "Montserrat", "Avenir";
    text-transform: uppercase;
    height: 100%;
    font-weight: 700;
    letter-spacing: 1px;
    color: steelblue;
    transition: all 0.3s;
    outline: none;
  }

  button:hover {
    color: white;
    background-color: steelblue;
  }

</style>
