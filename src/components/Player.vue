<script setup>
import videojs from "video.js"
import { onMounted,inject, watch } from "vue";
let player;
const tv = inject("active")
const toogleList = inject("toogleList")
onMounted(()=>{
    initializePlayer(tv)
})
watch(tv, (newSrc, oldSrc) => {
    player.src(newSrc.src) // Créer un nouveau lecteur avec la nouvelle source
});

const initializePlayer = function(tvitem) {
    tvitem =  tvitem.value ? tvitem.value : tvitem
    player = videojs("player", {
        sources: [{ 
            src:tvitem.src,
            preload:"metadata",
            responsive: true,
            type:"application/x-mpegURL"
        }],
        controls: true,
        autoplay: true,

    });
}


</script>

<template>
    <div class="videoPlayer" >
        <video class=" video-js" id="player" data-setup='{"fluid": true}' controls autoplay>
            <source>
        </video>
    </div>
</template>
<style>
.videoPlayer{
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: self-start;
    justify-content: center;
}
video{
    width: 100%;
}
@media screen and (max-width:800px){
    .videoPlayer{
        width: 100%;
        z-index: 0;
        background-color: white;
    }

}
</style>