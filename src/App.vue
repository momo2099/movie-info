<template>
  <Navbar />
  <Event :text="text" />
  <Movies 
  :data="data"
  @increaseLike="increaseLike($event)"
  @openModal="isModal=true; selectedMovie=$event"
  />
  <!-- The event name (custom event) triggered in the child component is prefixed with @ -->  
  <Modal 
  :data="data" 
  :isModal="isModal" 
  :selectedMovie="selectedMovie"
  @closeModal="isModal=false"
  />

</template>

<script>
// import the component wnat to bring in
import data from './assets/movies';
import Navbar from './components/Navbar.vue';
import Event from './components/Event.vue'; //이벤트 박스
import Modal from './components/Modal.vue';
import Movies from './components/Movies.vue'
console.log(data);
 
export default {
  name: 'App',
  data() {
    return {
      isModal: false,
      data: data,
      selectedMovie: 0,
      text: "HBO MAX",
    }
  },
  methods: {
    increaseLike(i) {
      this.data[i].like += 1;
    }
  },
    // Register the variable in the components section
    components: {
    Navbar: Navbar,
    Event: Event,
    Modal: Modal,
    Movies:Movies,
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
