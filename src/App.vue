<script>

import { store } from './store.js';
import axios from 'axios';
import AppSearch from './components/AppSearch.vue';
import AppContents from './components/AppContents.vue';

export default {
    components: {
        AppSearch,
        AppContents
    },

    data() {
        return {
          store
        };
    },

    methods: {
        getMovieFromApi() {
            let apiUrl = 'https://api.themoviedb.org/3/search/movie?api_key=25378c3a1e8ccece435091404e238d2c';
            const queryParams = {
                query: store.searchedMovie
            };

            if ( store.searchedMovie !== '') {
                axios.get(apiUrl, {
                params: queryParams
            }).then((response) => {
                store.movieList = response.data.results
            });
            };
        }
    }
}

</script>

<template>

    <AppSearch @searchMovie="getMovieFromApi()"></AppSearch>
    <main>
        <AppContents></AppContents>
    </main>

</template>

<style lang="scss">

    @use './style/generic';

</style>
