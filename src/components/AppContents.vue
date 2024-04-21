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
    },
    methods: {
        moviesHorizontalScroll(event) {
            event.preventDefault();
            const slider = this.$refs.moviesSlider;
            const content = this.$refs.movie;
            slider.scrollLeft += event.deltaY * 1.5;
        },
        seriesHorizontalScroll(event) {
            event.preventDefault();
            const slider = this.$refs.seriesSlider;
            const content = this.$refs.serie;
            slider.scrollLeft += event.deltaY * 3;
        }

    }
}

</script>

<template>

    <div v-if="store.searchedContent === ''">
        <h2 class="text-dark-emphasis text-center">I Film o le Serie Tv cercate saranno visualizzate qui.</h2>
    </div>

    <div class="container-xxl p-3 mb-5">
        <div class="row p-3">
            <template v-if="store.movieList.length > 0 || store.tvSeriesList.length > 0">

                <div v-if="store.movieList.length > 0">
                    <h2>Film</h2>
                </div>

                <div ref="moviesSlider" class="d-flex overflow-x-auto" @mousewheel="moviesHorizontalScroll">
                    <SingleCard ref="movies" v-for="movie in store.movieList" :key="movie.id" :cardInfo="movie">
                    </SingleCard>
                </div>

                <div v-if="store.tvSeriesList.length > 0" class="mt-3">
                    <h2>Serie Tv</h2>
                </div>

                <div ref="seriesSlider" class="d-flex overflow-x-auto" @mousewheel="seriesHorizontalScroll">
                    <SingleCard ref="serie" v-for="tvSerie in store.tvSeriesList" :key="tvSerie.id" :cardInfo="tvSerie">
                    </SingleCard>
                </div>

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