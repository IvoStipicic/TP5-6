<template>

  <section class="src-components-square">
    <div class="square" ref="square" :style="{backgroundColor: color}" @click="clickSquare"></div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-square',
    props: ['color'],
    mounted () {
    },
    data () {
      return {
      }
    },
    methods: {
      clickSquare() {
        this.$emit('onSquareSelected', this.color);
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">

  .square {
    width: 30%;
    background: blue;
    padding-bottom: 30%;
    float: left;
    margin: 1.66%;
    border-radius: 10%;
    transition: background 0.8s;
    -webkit-transition: background 0.8s;
    -moz-transition: background 0.8s;
  }

</style>
