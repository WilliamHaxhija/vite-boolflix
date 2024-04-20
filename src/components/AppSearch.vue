<script>

import { store } from '../store.js';

export default {
    name: 'AppSearch',

    data() {
        return {
            store
        };
    },
    methods: {
        getSelectedGenre() {
            store.selectedGenre = genre.name;
            return store.selectedGenre;
        }
    }
}

</script>

<template>

    <header class="fixed-top">
        <div class="container-fluid d-flex py-3 px-5 align-items-center">
            <h1 class="ms-5">BoolFlix</h1>
            <div class="d-flex flex-grow-1 justify-content-end me-5">
                <input @keyup.enter="$emit('searchContent')" v-model="store.searchedContent"
                    class="form-control me-3 p-2 h-25" type="text" placeholder="Search here...">
                <select v-model="store.selectedGenre" class="form-select me-3" aria-label="Default select example">
                    <option class="text-black-50" selected>Scegli un genere</option>
                    <option v-for="genre in store.genresList" :value="genre.name">{{ genre.name }}</option>
                </select>
                <button @click="$emit('searchContent')" type="button" class="btn btn-secondary h-25">Search</button>
            </div>
        </div>
    </header>

</template>

<style scoped lang="scss">
header {
    background-color: black;
}

h1 {
    color: rgb(163, 8, 8);
}

input {
    max-width: 40%;
}

select {
    max-width: 12%;
}
</style>