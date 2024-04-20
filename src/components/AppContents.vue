<script>

import { store } from '../store.js';
import SingleCard from './SingleCard.vue';

export default {
    name: 'AppContents',
    components: {
        SingleCard
    },

    data() {
        return {
            store
        };
    }
}

</script>

<template>

    <div v-if="store.searchedContent === ''">
        <h2 class="text-dark-emphasis">I Film o le Serie Tv cercate saranno visualizzate qui.</h2>
    </div>

    <div class="container p-3">
        <div class="row p-3">
            <template v-if="store.movieList.length > 0 || store.tvSeriesList.length > 0">

                <div v-if="store.movieList.length > 0">
                    <h2>Film</h2>
                </div>

                <SingleCard v-for="movie in store.movieList" :key="movie.id" :cardInfo="movie"></SingleCard>

                <div v-if="store.tvSeriesList.length > 0">
                    <h2>Serie Tv</h2>
                </div>

                <SingleCard v-for="tvSerie in store.tvSeriesList" :key="tvSerie.id" :cardInfo="tvSerie"></SingleCard>
                
            </template>
        </div>
    </div>

</template>

<style scoped lang="scss">

    h2 {
        color: white;
        text-align: left;
        margin: 1rem 0 2rem 2rem;
    }

</style>