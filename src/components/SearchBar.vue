<template lang="">
    <div class="search-box">
<!-- event.target.value: The value entered inside the corresponding element -->
        <input 
            type="search" 
            @change="
                $emit('searchMovie',$event.target.value);
                inputText=$event.target.value;
                $event.target.value='' "
                placeholder="검색어 입력"
            >
        <button>검색</button>
    </div>
    <p>{{ inputText }}</p>
</template>

<script>
export default {
 name:"SearchBarComponent",
 emits: ['searchMovie'], // Explicitly declare the event using the emits option
 data(){
    return{
        inputText:'',
    }
 },
 props:{
    data:Array,
 },

 watch:{
    inputText(name){
    // Check if the entered movie title exists in the data
        const findName=this.data.filter(movie=>{
            return movie.title.includes(name);
        })
        console.log(findName);
        if(findName.length==0){
            alert("No data available");
        }
    }
 }
}
</script>
<style>
  .search-box {
    padding: 10px;
    display: flex;
    justify-content: center;
  }

  .search-box input {
    padding: 5px 10px;
  }

  .search-box button {
    margin: 0;
  }
</style>