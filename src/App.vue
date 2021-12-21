<template>
  <div id="app">
    <carousel>
      <carousel-slide v-for="n in slides" :key="n" :index="n - 1">
        <div style="position: absolute; left: 0; right: 0; text-align:center; top: 50%; color: #FFF; font-size: 16px;"> Slide {{ n }} </div>    
        <img src="./assets/ig5.jpg" alt="" >
      </carousel-slide>
    </carousel>
    <div class="button">
      <button @click.prevent="addSlide" class="add">Ajouter un slide</button>
      <button @click.prevent="removeSlide" class="del">Supprimer un slide</button>
    </div>
  </div>
</template>

<script>
import Carousel from './components/carousel/Carousel.vue'
import CarouselSlide from './components/carousel/CarouselSlide.vue'

export default {
  name: 'App',
  data(){
    return{
      slides: 5,
    }
  },

  components: {
    Carousel,
    CarouselSlide
  },

  methods: {
    addSlide (){
      this.slides++
    },

    removeSlide(){
      if(this.slides > 1){
        this.slides--
      }
    }
  }
}
</script>

<style>
  img{
    display: block;
    width: 100%;
    height: 450px;
    margin: 0 auto;
  }
  body{
    margin: 0;
  }
  .button{
    width: 30%;
    margin: 5px auto;
  }
  .del, .add{
    display: inline-block;
    padding: 10px;
    font-size:12px;
    border-radius: 10px;
    color: #FFF;
    margin: 0 20px;
    font-weight: bold;
  }
  .del{
    background-color: red;
    margin-left: 10px;
  }
  .add{
    background-color: green;
    margin-left: 50px;
  }
</style>
