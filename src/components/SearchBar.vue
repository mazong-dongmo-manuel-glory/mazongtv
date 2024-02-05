<script setup>
import tv from './tv';

import { ref, computed, inject, watch } from "vue"
const tvlist = ref(tv)
const search = ref("")
const active = inject("active")
let toogleList = inject("toogleList")
const filteredTvList = computed(() => {
    return tvlist.value.filter(tvitem => tvitem.name.toLowerCase().includes(search.value.toLowerCase()))
})
function handleClick(key) {
    active.value = tvlist.value.filter(tvitem => tvitem.name == key)[0]
}
watch(toogleList, () => {
    console.log(toogleList.value)
})
</script>

<template>
    <div class="searchBar" v-if="toogleList">
        <div class="searchZone">
            <span class="material-symbols-outlined" @click="() => { toogleList = !toogleList }">close</span>

            <a href="/" class="logo">
                <img src="../assets/tv.svg" alt="logo" title="tv">
            </a>
            <div class="inputZone">
                <input v-model="search">
                <span class="material-symbols-outlined">search</span>
            </div>
        </div>
        <ul class="tvlist">

            <li v-for="tvitem in  filteredTvList" :data-src="tvitem.src" :key="tvitem.name"
                @click="handleClick(tvitem.name)">
                <img :src="tvitem.logo" :alt="tvitem.name" :title="tvitem.name">
                <span>{{ tvitem.name }}</span>
            </li>

        </ul>
    </div>
</template>
<style>
.logo img {
    width: 60px;
}

.searchBar {
    height: 100vh;
    width: 20%;
    box-shadow: rgba(0, 0, 0, 0.2) 0px 18px 50px -10px;
    overflow-y: auto;
    position: absolute;
    z-index: 1;
    background-color: white;
}

.searchZone {
    position: sticky;
    top: 0;
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    width: 100%;
    padding: 5px;
    background-color: white;
    z-index: 1;

}

.inputZone {
    width: 100%;
    border: 1px solid rgb(224, 224, 224);
    display: flex;
    border-radius: 5px;
    height: 50px;
    align-items: center;
    padding: 5px;
}

.inputZone * {
    font-size: 2rem;
}

.inputZone span {
    cursor: pointer;
    padding-top: 10px;

}

.inputZone input {
    width: 100%;
    height: 70%;
    vertical-align: middle;
}

.tvlist {
    list-style: none;
    position: relative;
    padding: 0;
    display: flex;
    flex-direction: column;
    background: white;
    z-index: 0;
}

.tvlist li {
    cursor: pointer;
    border-bottom: 1px solid rgb(224, 224, 224);
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 5px 0;
    flex-direction: column;
    transition: opacity 0.5s;
}

.tvlist li>span {
    font-weight: bolder;
    text-transform: uppercase;
}

.tvlist li:last-child {
    border-bottom: none;

}

li img {
    width: 40px;
}

li:hover {
    opacity: 0.7;
}

.close {
    display: none;
}

@media screen and (max-width:800px) {
    .searchBar {
        position: fixed;
        width: 70%;
        z-index: 3;
        background-color: white;
    }

    .close {
        display: flex;
        align-self: self-end;
        justify-items: flex-end;
        justify-content: flex-start;
        float: right;
        padding: 5px;
        font-size: 3rem;
    }

}</style>