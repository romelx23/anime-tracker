<script lang="ts" setup>
import { MyAnime } from "../../interfaces/anime";

const props = defineProps<{
    my_anime_sort: MyAnime[],
    deleteAnime: (id: number) => void,
    increaseWatched: (anime: MyAnime) => void,
    decreaseWatched: (anime: MyAnime) => void,
}>()
</script>

<template>
    <h2 v-if="my_anime_sort.length > 0">Mi Lista de Anime</h2>
    <ul class="list-anime">
        <li class="list-anime-item" v-for="(anime, index) in my_anime_sort" :key="anime.id">
            <div class="flex-title">
                <h2>({{  index + 1  }})</h2>
                <img :src="anime.image" :alt="anime.title">
            </div>
            <div class="flex-column content-title">
                <p class="title">Título</p>
                <h2>{{  anime.title  }}</h2>
            </div>
            <div class="flex-column">
                <p class="title">Capítulos</p>
                <p>{{  anime.watched_episodes  }} / {{  anime.total_episodes  }}</p>
            </div>
            <div class="flex-column">
                <p class="title">Acciones</p>
                <div class="flex">
                    <button :disabled="anime.watched_episodes <= 0" @click="decreaseWatched(anime)">
                        <i class="fas fa-minus"></i>
                    </button>
                    <button :disabled="anime.total_episodes === anime.watched_episodes" @click="increaseWatched(anime)">
                        <i class="fas fa-plus"></i>
                    </button>

                    <button @click="deleteAnime(anime.id)">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>
            </div>
        </li>
    </ul>
</template>

<style scoped>
.flex-column {
    /* width: 100%; */
    display: flex;
    flex-direction: column;
    align-items: left;
}

.flex {
    display: flex;
}

.flex-title {
    display: flex;
    flex-direction: row;
    align-items: center;
}

.content-title {
    width: 100%;
}

.flex .title {
    font-size: 0.8rem;
    font-weight: 600;
    margin: 0;
}

.flex p {
    font-size: 1rem;
    font-weight: 600;
}

.list-anime {
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 70vh;
    overflow-y: auto;
    gap: 20px;
}

.list-anime-item {
    /* width: 100%; */
    height: 200px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
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
    font-size: 1.2rem;
    /* margin: 0 1em; */
}

button {
    background-color: #e4008c;
    border: none;
    cursor: pointer;
    font-size: 1rem;
    padding: 8px 10px;
    border-radius: 5px;
    margin-left: 5px;
}

@media screen and (max-width:768px) {
    .list-anime-item {
        height: auto;
        display: grid;
        padding-top: 20px;
        grid-template-columns: 1fr 1fr;
        position: relative;
    }

    .list-anime-item img {
        height: 150px;
    }

    .list-anime-item h2 {
        font-size: 1rem;
        margin: 0;
    }

    .flex-title {
        flex-direction: column;
        align-items: flex-start;
    }

    .flex-title h2 {
        position: absolute;
        text-align: center;
        grid-column: 1/3;
    }

    .flex-column .title {
        font-weight: 700;
        margin: 10px 0;
    }
}

@media screen and (max-width:500px) {
    .list-anime-item {
        height: auto;
        display: grid;
        padding-top: 20px;
        grid-template-columns: 1fr;
        position: relative;
    }
}
</style>