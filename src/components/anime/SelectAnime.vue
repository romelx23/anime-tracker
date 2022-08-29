<script lang="ts" setup>
import { onMounted } from "@vue/runtime-core";
import { Anime } from "../../interfaces/anime";

const props = defineProps<{
  animes: Anime[],
  addAnime: (anime: Anime) => void,
}>()
onMounted(() => {
  console.log(props.animes);
})
</script>

<template>
  <ul :class="[props.animes.length > 0 ? 'list-anime' : 'hidden', 'animation-height']">
    <li class="list-anime-item" v-for="anime in animes" :key="anime.mal_id">
      <img :src="anime.images.jpg.image_url" alt="">
      <h2>{{  anime.title  }}</h2>
      <p>{{  anime.episodes  }}</p>
      <button class="button-anime" @click="addAnime(anime)">
        <i class="fas fa-plus"></i>
      </button>
    </li>
  </ul>
</template>

<style scoped>
/* .list-anime {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.list-anime-item {
  width: 200px;
  height: 350px;
  margin: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
}

.list-anime-item img {
  width: 100%;
  height: 260px;
  object-fit: cover;
}

.list-anime-item h2 {
  font-size: 1.2rem;
  font-weight: 600;
  margin: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

.list-anime-item p {
  font-size: 1rem;
  font-weight: 400;
  margin: 0;
}

@media screen and (min-width: 768px) { */
.animation-height {
  transition: height 0.5s ease;
}

.list-anime {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  height: 70vh;
  margin: 20px 0;
  overflow-y: auto;
  gap: 20px;
}

.hidden {
  height: 0;
  overflow: hidden;
  visibility: hidden;
}

.list-anime-item {
  /* width: 100%; */
  height: 200px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;

  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px 30px;
}

.list-anime-item img {
  width: 100px;
  height: 120px;
  object-fit: cover;
}

.list-anime-item h2 {
  width: 100%;
  text-align: left;
  margin: 0 1em;
  font-size: 1.2rem;
}

.button-anime {
  background-color: #e4008c;
  border: none;
  cursor: pointer;
  font-size: 1rem;
  padding: 8px 10px;
  border-radius: 5px;
  margin-left: 5px;
}

/* } */
</style>