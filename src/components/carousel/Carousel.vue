<template>
  <div class="carousel">
    <slot></slot>
    <button class="carousel__nav carousel__next" @click.prevent="next">Next</button>
    <button class="carousel__nav carousel__prev" @click.prevent="previows">Prev</button>

    <div class="carousel__pagination">
      <button v-for="n in slides" :key="n.index" @click.prevent="goto(n.index)" :class="{active: n.index == index}"></button>
    </div>
  </div>
  
  
</template>

<script>
export default {
  data () {
    return {
      index: 0,
      slides: [],
      direction: 'right'
    }
  },

  mounted() {
    this.slides = this.$children
  },

  computed: {
    slidesCount() {
      return this.$parent.slides
    }
  },

  methods: {
    next(){
      this.direction = 'right'
      if(this.index < this.slidesCount - 1){
        this.index++
      }
      else{
        this.index = 0
      }
    },
    
    previows() {
      this.direction = 'left'
      if(this.index > 0){
        this.index--
      }
      else{
        this.index = this.slidesCount - 1
      }
    },

    goto(index){
      this.direction = index > this.index ? 'right' : 'left'
      this.index = index
    }
  },

  watch: {
    slides(){
      if(this.index >= this.slidesCount - 1){
        this.index = this.slidesCount - 1
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .carousel{
    position: relative;
    overflow: hidden;
  }
  .carousel__nav{
    position: absolute;
    top: 50%;
    left: 10px;
  }
  .carousel__nav.carousel__next{
    right: 10px;
    left: auto;
  }
  .carousel__pagination{
    position: absolute;
    bottom: 10px;
    left: 0;
    right: 0;
    text-align: center;
  }
  .carousel__pagination button{
    display: inline-block;
    width: 25px;
    height: 25px;
    background-color: #000;
    opacity: 0.8;
    border-radius: 25px;
    margin: 0 5px;
  }
  .carousel__pagination button.active{
    background-color: #FFF;
  }
</style>
