<template>
  <div class="heroes">
    <div class="hero" v-for="character in characters" :key="character.id">
      <h2 class="characterName">{{ character.name }}</h2>
      <img class="imagen" :src="character.thumbnail.path + '.' + character.thumbnail.extension" alt="" >
    </div>
  </div>
</template>
  

<script setup>
  import axios from "axios";
  const Hash = '9efaf282a664b7c0cd67ff952200b0d2';
  const publicKeys = '14c7fd83deec0e48b20476608beb39ca';
  
  const characters = ref([]);
  
  const loadCharacter = async ()=>{
    const url = `https://gateway.marvel.com:443/v1/public/characters?limit=100&ts=1&apikey=${publicKeys}&hash=${Hash}`;
    const { data } = await axios.get(url);
    console.log(data.data.results)
    const charactersWithImage = data.data.results.filter(character => {
      return character.thumbnail.path != "http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available"
    });
    characters.value=charactersWithImage;
    console.log(charactersWithImage)
  }
  loadCharacter();
</script>