<script>

import { store } from '../store.js';
import SingleMovie from './SingleMovie.vue';
import SingleTvSerie from './SingleTvSerie.vue';

export default {
    name: 'AppContents',
    components: {
        SingleMovie,
        SingleTvSerie
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
            <template v-if="store.movieList.length > 0 || store.tvSeriesList.length > 0">
                <SingleMovie v-for="movie in store.movieList" :key="movie.id" :movieInfo="movie"></SingleMovie>
                <SingleTvSerie v-for="tvSerie in store.tvSeriesList" :key="tvSerie.id" :tvSerieInfo="tvSerie"></SingleTvSerie>
            </template>
        </div>
    </div>

</template>

<style scoped lang="scss"></style>