<script setup>
import axios from "axios";
import { ref } from 'vue';
import SiteModal from '../components/SiteModal.vue';
const showModal = ref(false);
const selectedId = ref(0);
const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};
const closeModal = () => {
  showModal.value = false;
};
let data = (await axios.get("https://api.themoviedb.org/3/trending/movie/week", {
    params: {
        api_key: "bcc37e055784982d779add0faa5de9c2"
    }
})).data.results;
console.log(data)
</script>

<template>
   <div>
      <h1> HERES SOME OF OUR WONDERFULL COLLECTION</h1>
 
    </div>

    <div>
        <img v-for="movie in data" @click="openModal(movie.id)" class="poster" :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
    </div>
    <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
</template>

<style scoped>
 h1 {
    color: rgb(255, 0, 0);
    border-color: rgb(0, 0, 0);
    border-width: 15px;
    border-style:dashed;
    font-family:'Times New Roman', Times, serif;
    padding: 20px;
    font-size: 25px;
   }
   
 

img {
  width: 315px; 
  border-style:groove;
  border-color: rgb(0, 0, 0);
  border-width: 15px;
  margin-right: 10px;
  margin-top: 15px;


}

</style>

