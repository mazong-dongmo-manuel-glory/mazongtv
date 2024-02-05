<script setup>
 import SearchBar from './components/SearchBar.vue';
 import Player from './components/Player.vue';
 import tvlist from "./components/tv"
 import {ref,provide} from "vue";
 const tv = ref(tvlist[0])
 const toogleList = ref(true)
 provide("active",tv)
 provide("toogleList",toogleList)
</script>
<template>
<div class="header">
  <span class="material-symbols-outlined menu" @click="()=>{toogleList = !toogleList}">menu</span>
</div>
<SearchBar></SearchBar>
<Player></Player>
</template>
<style>
#app{
  display: flex;
  flex-direction: column;
}
.menu{
  padding: 5px;
  font-size: 2rem;
}
</style>