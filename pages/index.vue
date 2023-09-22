<template>
  <div class="heroes">
    <div class="hero" v-for="character in characters" :key="character.id"  @click="showCharacterDetails(character)">
      <h2 class="characterName">{{ character.name }}</h2>
      <img class="imagen" :src="character.thumbnail.path + '.' + character.thumbnail.extension" alt="" >
    </div>
    <div v-if="selectedCharacter" class="desactivar-fondo">
    <div v-if="selectedCharacter" class="modal">
      <button @click="closeDialog" class="close-button">X</button>
      <h2 class="titulosuper">{{ selectedCharacter.name }}</h2>
      <img class="peque" :src="selectedCharacter.thumbnail.path + '.' + selectedCharacter.thumbnail.extension" alt="">
      <p class="texto">{{ selectedCharacter.description }}</p>
      <p>Cantidad de comics: {{ selectedCharacter.comics.available }}</p>
      <p>Cantidad de series: {{ selectedCharacter.series.available }}</p>
      <p>Cantidad de historias: {{ selectedCharacter.stories.available }}</p>
      <p>Cantidad de eventos: {{ selectedCharacter.events.available }}</p>
      <h3>Series en las que aparecio:</h3>
      <ul>
        <li v-for="series in selectedCharacter.series.items.slice(0, 3)" :key="series.name">{{ series.name }}</li>
      </ul>
    </div>
  </div>
  </div>
</template>
  

<script setup>
import { ref } from 'vue';
  import axios from "axios";
  const Hash = '9efaf282a664b7c0cd67ff952200b0d2';
  const publicKeys = '14c7fd83deec0e48b20476608beb39ca';
  
  const characters = ref([]);
  const selectedCharacter = ref(null);
  
  const loadCharacter = async ()=>{
    const url = `https://gateway.marvel.com:443/v1/public/characters?limit=100&nameStartsWith=S&ts=1&apikey=${publicKeys}&hash=${Hash}`;
    const { data } = await axios.get(url);
    console.log(data.data.results)
    const charactersWithImage = data.data.results.filter(character => {
      return character.thumbnail.path != "http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available" & character.description != ""
    });
    characters.value=charactersWithImage;
    console.log(charactersWithImage)
  }
  const showCharacterDetails = (character) => {
  selectedCharacter.value = character;
  console.log("sapo")
}

const closeDialog = () => {
  selectedCharacter.value = null;
}
  loadCharacter();
</script>