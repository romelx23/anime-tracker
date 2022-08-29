<script lang="ts" setup>

const props = defineProps<{
    query: string;
    handleSearch: (e: any) => void;
    searchAnime: () => void;
}>()
</script>

<template>
    <form action="" @submit.prevent="searchAnime">
        <input class="input-search" type="text" placeholder="Buscar anime...!" v-model="query" @input="handleSearch">
        <button type="submit" class="button-anime">
            <i class="fas fa-search"></i>
        </button>
    </form>
</template>

<style scoped>
form {
    width: 100%;
    display: flex;
    justify-content: center;
}

.input-search {
    max-width: 100%;
    width: 80%;
    height: 2em;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 0.5em;
    font-size: 1.2em;
    padding-left: 1em;
}

.button-anime {
    /* background-color: #fff; */
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 0.5em;
    font-size: 1.2em;
    padding: 0 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}
</style>