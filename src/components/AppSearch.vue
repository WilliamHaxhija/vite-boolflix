<script>

import { store } from '../store.js';

export default {
    name: 'AppSearch',

    data() {
        return {
            store,
            navs: ['Home', 'Film', 'Serie Tv', 'New', 'My List'],
            activeNav: 0
        };
    },
    methods: {
        getSelectedGenre() {
            store.selectedGenre = genre.name;
            return store.selectedGenre;
        },
        activateNavElement(index) {
            this.activeNav = index;
        }
    }
}

</script>

<template>

    <header class="fixed-top">
        <div class="container-fluid d-flex py-3 px-5 align-items-center">
            <h1 class="ms-5">BoolFlix</h1>
            <nav class="d-flex align-items-center">
                <ul class="d-flex align-items-center text-white">
                    <li v-for="nav, index in navs" :class="{active: activeNav === index}" @click="activateNavElement(index)">{{ nav }}</li>
                </ul>
            </nav>
            <div class="d-flex flex-grow-1 justify-content-end me-5">
                <input @keyup.enter="$emit('searchContent')" v-model="store.searchedContent"
                    class="form-control me-3 p-2 h-25 border border-dark" type="text"
                    placeholder="Search here...">
                <select v-model="store.selectedGenre" class="form-select bg-dark me-3 border border-dark">
                    <option class="text-white-50" selected>Scegli un genere</option>
                    <option v-for="genre in store.genresList" :value="genre.name">{{ genre.name }}</option>
                </select>
                <button @click="$emit('searchContent')" type="button" class="btn btn-dark h-25">Search</button>
            </div>
        </div>
    </header>

</template>

<style scoped lang="scss">
header {
    background-color: rgba(0, 0, 0, 0.953);
    box-shadow: rgb(36, 36, 36) 0px 20px 30px -10px;
}

h1 {
    color: rgb(163, 8, 8);
    letter-spacing: 7px;
    font-weight: 700;
}

input {
    max-width: 35%;
}

select {
    max-width: 15%;
    cursor: pointer;
    color: white;
}

nav {
    margin-left: 3rem;
}

ul {
    list-style: none;
    padding: 0;
    margin: 0;

    li {
        margin-right: 1.3rem;
        font-weight: 600;
        cursor: pointer;
        &:hover {
            color: rgb(225, 3, 3);
            transform: scale(1.1);
            transition: 0.2s;
        }
    }
}

.active {
    color: rgb(225, 3, 3);
}

</style>