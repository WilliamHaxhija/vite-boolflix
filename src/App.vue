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
                query: store.searchedContent
            };

            if (store.searchedContent !== '') {
                axios.get(apiUrl, {
                    params: queryParams
                }).then((response) => {
                    store.movieList = response.data.results
                });
            };
        },
        getTvSerieFromApi() {
            let apiUrl = 'https://api.themoviedb.org/3/search/tv?api_key=25378c3a1e8ccece435091404e238d2c';
            const queryParams = {
                query: store.searchedContent
            };

            if (store.searchedContent !== '') {
                axios.get(apiUrl, {
                    params: queryParams
                }).then((response) => {
                    store.tvSeriesList = response.data.results
                });
            };
        },
        getContentsFromApi() {
            this.getMovieFromApi();
            this.getTvSerieFromApi();
        },
        getGenresFromApi() {
            let apiUrl = 'https://api.themoviedb.org/3/genre/movie/list?api_key=25378c3a1e8ccece435091404e238d2c';
            axios.get(apiUrl).then((response) => {
                store.genresList = response.data.genres;
            });
        }
    },
    mounted() {
        this.getGenresFromApi()
    }
}

</script>

<template>

    <AppSearch @searchContent="getContentsFromApi()"></AppSearch>

    <main>
        <AppContents></AppContents>
    </main>

</template>

<style lang="scss">
@use './style/generic';

main::-webkit-scrollbar-track {
    background-color: #5a5a5a;
    border-radius: 50px;
}

main::-webkit-scrollbar-thumb {
    background-color: #a3a3a3;
    border-radius: 50px;
}
</style>
