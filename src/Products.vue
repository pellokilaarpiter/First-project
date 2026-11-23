<script setup>
import { ref, reactive, computed, watch } from "vue";

// const data = {link: "www.facebook.com", name: "facebook",imgUrl: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSSg1vk_HU23lIVOGsLbd2RtnbF-q0AcUOa3AnWDvlayqC5PLXBUawHBJpyQExl_EnFEJplbyHQkGZZffOUdbeGLN_Go4EZAMXFTt3q5xIU&s=10", altText:"Captain America", value: "Dari Mr. aja", }

const presiden = [
  { nama: "Soekarno", periode: "1945-1970", wakil: "Mohammad Hatta" },
  { nama: "Soeharto", periode: "1970 - 2000", wakil: "Habibie" },
  { nama: "Habibie", periode: "2000 - 2001", wakil: "Megawati" },
];
</script>

<template>
  <div v-for="(item, index) in presiden" :key="index">
    <h2>{{ item.nama }}</h2>
    <p>wakil : {{ item.wakil }}</p>
    <p>periode : {{ item.periode }}</p>
  </div>
  <!-- <a :href="data.link"> {{ data.name }}    </a>
  <img :src="data.imgUrl" :alt="data.altText">
  <input type="text" :value="data.value"> -->
</template>

<style scoped></style>
