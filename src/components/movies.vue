<template>
    <div class="container">
        <h1>영화정보</h1>
        <div v-for="(movie, i) in data" :key="i" class="item">
            <figure>
                <img :src="`${movie.imgUrl}`" :alt="`${movie.title}`">
            </figure>

            <div class="info">
                <h3 class="bg-yellow">{{ movie.title }}</h3>
                <p>개봉: {{ movie.year }}</p>
                <p>장르: {{ movie.category }}</p>
                <!-- {{ movie.like }} <button @:click="increaseLike(i)">좋아요</button> -->
                {{ movie.like }} <button @:click="$emit('increaseLike',i)">좋아요</button>  
                <p><button @click="$emit('openModal',i)">상세보기</button></p>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: "MoviesComponent",
    
    //부모 -> 자식
    props: {
        data: Array,
    }
}
</script>
<style>
  .container {
    padding: 20px;
  }
</style>