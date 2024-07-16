<script setup>
import { ref } from "vue";

const info = ref({
  id: null,
  dados: [],
  personagens: [],
});

async function getData() {

  const response =
    await fetch(`https://rickandmortyapi.com/api/character/?name=${info.value.personagem}`);
  const data = await response.json();
  // console.log(data);

  for (const item of data.results) {
    info.value.dados.push({
      personagem: item.name,
      img: item.image,
      genero: item.gender,
      especie: item.species,
      local: item.location.name,
      origem: item.origin.name,
      status: item.status,
    });

  }
}
</script>

<template>
  <div class="container">
    <h1>Pesquise o personagem</h1>

  <div class="trazer_info"> 
  <div class="input"> 
  <input v-model="info.personagem" type="text" class="input" />
</div>
  <div class="btn">
    <button @click="getData">Clique</button>
  </div>
</div>
<div class="conteudo"> 
  <div v-for="personagem in info.personagens" :key="personagem.personagem">
    <p>{{ personagem.personagem }}</p>
  </div>

  <div class="personagens" v-for="item in info.dados" :key="item.genero">
    <div class="personagem"> 
    <p class="nome" > {{ item.personagem }}</p>
  </div>
  <div class="img"> 
    <img :src="item.img" alt="">
  </div>
  <div class="infos"> 

  <div class="genero"> 
    <p id="genero" > <span> Gênero:</span>  {{ item.genero }}</p>
  </div>
  <div class="especie"> 
    <p><span> Espécie:</span> {{ item.especie }}</p>
  </div>
  <div class="local"> 
    <p><span> Local:</span> {{ item.local }}</p>
  </div>
  <div class="origem">
    <p><span> Origem:</span> {{ item.origem }}</p>

  </div>
  <div class="status"> 
    <p><span> Status:</span> {{ item.status }}</p>
  </div>
  </div>
  </div>
</div>
</div>

</template>

<style scoped></style>
