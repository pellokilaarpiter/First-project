<script setup>
import { ref } from "vue";
import Navbar from "./components/Navbar.vue";

const a = 0;
let name = "Santi";

const count = ref(0);

const imgUrl = "https://in.pinterest.com/pin/622059767326415693/";
</script>

<template>
  <!-- <h1>You did it!</h1>
  <p>
    <h2>hello {{ name }}</h2>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>
  
  <button @click="count--">-</button>
  <p >{{ count }}</p>
  <button @click="count++">+</button>
<img :src="imgUrl" alt=""> -->



  <Navbar />
  <RouterView />

</template>

<style scoped>
h2 {
  color: red;
}
</style>
