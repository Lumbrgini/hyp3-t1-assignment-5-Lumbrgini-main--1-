<script setup>
import { ref } from "vue";

const API_URL = "https://randomuser.me/api";
const API_URL_Photo = "https://robohash.org/set_set5/";

// reactive data
const name = ref("Person name"); // name.value
const imgSrc = ref("");          // imgSrc.value

const defaultName = "Default name";
const defaultPhoto = "https://static.wikia.nocookie.net/untitled-utmm-game/images/d/d2/Bruh_Core_Icon.png/revision/latest/scale-to-width-down/382?cb=20210517005916";
// methods

async function gnrPersonName() {
  try {
    const response = await fetch(API_URL);
    const data = await response.json();
    name.value = data.results[0].name.first + " " + data.results[0].name.last;
  } catch (error) {
      console.error("Error fetching " + API_URL, error);
      name.value = defaultName;
    }
}

async function gnrPersonPhoto() {
  try {
    const combinedName = name.value.split(" ").join("");
    imgSrc.value = API_URL_Photo + combinedName + ".png";
  } catch (error) {
      console.error("Error fetching " + API_URL_Photo, error);
      imgSrc.value = defaultPhoto;
    }
}

async function generatePerson() {
  await gnrPersonName();
  await gnrPersonPhoto();
  console.log(imgSrc.value);
}
</script>

<template>
  <h2>{{ name }}</h2>
  <img :src="imgSrc" alt="Click 'Create' to generate look!"><br>
  <button @click="generatePerson">Create</button>
</template>

<style scoped>
</style>