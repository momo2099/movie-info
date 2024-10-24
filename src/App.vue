<template>
  <Navbar />
  <Event :text="text[eventTextNum]" />
  <Searchbar :data="data_temp" @searchMovie="searchMovie($event)"/>
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>
  <Movies :data="data_temp" @increaseLike="increaseLike($event)" @openModal="isModal = true; selectedMovie = $event" />
  <!-- The event name (custom event) triggered in the child component is prefixed with @ -->
  <Modal :data="data" :isModal="isModal" :selectedMovie="selectedMovie" @closeModal="isModal = false" />

</template>

<script>
// import the component wnat to bring in
import data from './assets/movies';
import Navbar from './components/Navbar.vue';
import Event from './components/Event.vue'; // event box
import Modal from './components/Modal.vue';
import Movies from './components/Movies.vue';
import Searchbar from './components/SearchBar.vue';//SearchBar

console.log(data);

export default {
  name: 'App',
  data() {
    return {
      isModal: false,
      data: data, // Original
      data_temp: [...data], // Copy
      selectedMovie: 0,
      text: [ 
        'NETPLIX 강렬한 운명의 드라마, 경기크리처',
        '디즈니 100주년 기념작, 위시',
        '그날, 대한민국의 운명이 바뀌었다, 서울의 봄',
      ],
      eventTextNum:0,
      interval:null,
    }
  },
  methods: {
    increaseLike(id) {
      this.data.find(movie=>{
        if(movie.id==id){
          movie.like+=1;
        }
      })
    },

  // Fetch data that includes the movie title
    searchMovie(title){
      this.data_temp=this.data.filter(movie=>{
        return movie.title.includes(title);
      })
    },
    showAllMovie(){
      this.data_temp=[...this.data]
    }
  },

  // Register the variable in the components section
  components: {
    Navbar: Navbar,
    Event: Event,
    Modal: Modal,
    Movies: Movies,
    Searchbar: Searchbar
  },
  mounted(){
    console.log('mounted');
    this.interval=setInterval(() =>{
      if(this.eventTextNum==this.text.length-1){
        this.eventTextNum=0;
      }else{
        this.eventTextNum+=1;
      }
    },2000)
  },
  unmounted(){
    clearInterval(this.interval); // clear interval
  }

}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  max-width: 768px;
  margin: 0 auto;
  padding: 20px;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

button {
  margin-right: 10px;
  margin-top: 1rem;
}

.item {
  width: 100%;
  border: 1px solid #ccc;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
}

.item .info {
  width: 100%;
}
</style>
