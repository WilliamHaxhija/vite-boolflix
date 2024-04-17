<script>

import { store } from '../store.js';
import SingleMovie from './SingleMovie.vue';

export default {
    name: 'AppContents',
    components: {
        SingleMovie
    },

    data() {
        return {
            store
        };
    }
}

</script>

<template>

    <div class="container">
        <div class="row">
            <template v-if="store.movieList.length > 0">
                <SingleMovie v-for="movie in store.movieList" :key="movie.id" :movieInfo="movie"></SingleMovie>
            </template>
        </div>
    </div>

</template>

<style scoped lang="scss"></style>