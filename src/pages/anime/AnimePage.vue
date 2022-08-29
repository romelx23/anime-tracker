<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { onMounted, ref } from 'vue';
import SearchAnime from '../../components/anime/SearchAnime.vue';
import SelectAnime from '../../components/anime/SelectAnime.vue';
import { Anime, AnimeResponse, MyAnime } from '../../interfaces/anime';
import MyListAnime from '../../components/anime/MyListAnime.vue';
// los animes que selecciono
const my_anime = ref<MyAnime[]>([]);
// la variable que contiene mi busqueda
const query = ref('');
// los animes que busco
const animes = ref<Anime[]>([]);
// error de busqueda
const error_search = ref(false);

const my_anime_sort = computed(() => {
    return my_anime.value.sort((a, b) => {
        return a.title.localeCompare(b.title);
    });
});

const searchAnime = async () => {
    const url = 'https://api.jikan.moe/v4/anime?q=' + query.value;
    try {
        const res = await fetch(url);
        const { data }: AnimeResponse = await res.json();
        animes.value = data;
        console.log(query.value);
        error_search.value = false;
    } catch (error) {
        error_search.value = true;
        // console.log(error);
        // console.log(data);
    }
}

const handleSearch = (e: any) => {
    if (!e.target.value) animes.value = [];
    query.value = e.target.value;
    error_search.value = false;
    // console.log(query.value);
    // searchAnime();
}

const addAnime = (anime: Anime) => {
    console.log(anime);
    animes.value = [];
    query.value = '';
    my_anime.value.push({
        id: anime.mal_id,
        title: anime.title,
        image: anime.images.jpg.image_url,
        total_episodes: anime.episodes,
        watched_episodes: 0,
    });
    localStorage.setItem('my_anime', JSON.stringify(my_anime.value));
}

const deleteAnime = (id: number) => {
    my_anime.value = my_anime.value.filter((anime) => anime.id !== id);
    localStorage.setItem('my_anime', JSON.stringify(my_anime.value));
}

const increaseWatched = (anime: MyAnime) => {
    anime.watched_episodes++;
    localStorage.setItem('my_anime', JSON.stringify(my_anime.value));
}
const decreaseWatched = (anime: MyAnime) => {
    if (anime.watched_episodes > 0) anime.watched_episodes--;
    localStorage.setItem('my_anime', JSON.stringify(my_anime.value));
}

onMounted(() => {
    const my_anime_local = localStorage.getItem('my_anime');
    if (my_anime_local) my_anime.value = JSON.parse(my_anime_local);
});

</script>

<template>
    <div class="container-anime">
        <h1>Página para buscar su anime 😏</h1>
        <SearchAnime :query="query" :handleSearch="handleSearch" :searchAnime="searchAnime" />
        <p v-if="query.length > 0 && !error_search">
            <span>Buscando: </span>
            <span>{{  query  }}</span>
        </p>
        <p v-if="error_search && animes.length === 0">
            <span>No se encontró</span>
        </p>
        <SelectAnime :animes="animes" :addAnime="addAnime" />
        <MyListAnime :my_anime_sort="my_anime_sort" :increase-watched="increaseWatched"
            :decrease-watched="decreaseWatched" :deleteAnime="deleteAnime" />
        />
    </div>
</template>

<style scoped>
.container-anime {
    /* width: 100%; */
    padding: 0 20px 0 20px;
    height: 100%;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>