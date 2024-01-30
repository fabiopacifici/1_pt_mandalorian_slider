<script>
export default {
  /* Options object */
  name: 'App',
  /* Data option */
  data() {
    return {
      activeImage: 0,
      autoplay: null,
      slider: {
        name: 'Mandalorian',
        images: [
          'https://image.tmdb.org/t/p/original/9zcbqSxdsRMZWHYtyCd1nXPr2xq.jpg',
          'https://image.tmdb.org/t/p/original/aZ4fmjMUAhS6PWhVLDDfT0RAdNe.jpg',
          'https://image.tmdb.org/t/p/original/p7fwOnlxYYlB4A8U2b0JfX21Rr1.jpg',
          'https://image.tmdb.org/t/p/original/qruRhG6jE5M8lWnW1AGOBxtdmCO.jpg',
          'https://image.tmdb.org/t/p/original/lMu3y10KgIYtXFPeCMim3D8iihV.jpg'

        ],
        category: 'Action',
        length: 40,
      }
    }
  },
  methods: {
    prev() {
      console.log('prev');
      this.activeImage--;

      if (this.activeImage < 0) {
        this.activeImage = this.slider.images.length - 1;
      }

    },
    next() {
      console.log('next');
      this.activeImage++;
      if (this.activeImage > this.slider.images.length - 1) {
        this.activeImage = 0;
      }
    }
  },
  mounted() {

    console.log(this.slider);
    this.autoplay = setInterval(()=>{
      this.next();
    }, 1000)
  }
}
</script>

<template>
  <header>
    <h1>PAge header</h1>
  </header>

  <main>


    <div class="container">
      <h1>{{ slider.name }}</h1>


      <div class="slides">
        <img :src="slider.images[activeImage]" alt="">
      </div>

      <div class="thumbs">

        <img v-for="(thumb, index) in slider.images" :src="thumb" width="100" alt=""
          :class="index === activeImage ? 'active' : ''" @click="activeImage = index" :key="'thumb' + index">


      </div>


      <div class="navigator">
        <button class="prev" @click="prev">Prev</button>
        <button class="next" @click="next">Next</button>
      </div>
    </div>
  </main>

  <footer>
    <p>Footer here</p>
  </footer>
</template>

<style>
*
{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

img
{
  max-width: 100%;
}

.container
{
  width: 70%;
  max-width: 1176px;
  margin: auto
}

.row
{
  display: flex;
  flex-wrap: wrap;
  margin: 0 -1rem
}

.col
{
  width: auto;
  flex-basis: auto;
  padding: 1rem
}

.slides
{
  & > img
  {
    border-radius: 1rem;
  }
}


.thumbs {
  display: flex;
  justify-content: space-evenly;
  & > img.active {
    border: 4px solid black;
  }
}


.navigator
{
  margin-top: 1rem;
  display: flex;
  justify-content: space-between;

  & > button
  {
    display: inline-block;
    border-radius: 1rem;
    padding: 0.25rem 0.75rem;
    border-style: none;
   &:hover {
    cursor: pointer;
   }
  }
}
</style>
