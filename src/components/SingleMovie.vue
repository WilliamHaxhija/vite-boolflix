<script>

import { store } from '../store.js';

export default {
    name: 'SingleMovie',
    props: {
        movieInfo: Object
    },

    data() {
        return {
            store
        };
    }
}

</script>

<template>

    <div class="col-3">
        <div class="ms-infos">
            <div>{{ movieInfo.title }}</div>
            <div>{{ movieInfo.original_title }}</div>

            <div v-if="movieInfo.original_language === 'en'">
                <img src="../assets/img/flag-uk.png" alt="en-flag">
            </div>
            <div v-else-if="movieInfo.original_language === 'fr'">
                <img src="../assets/img/flag-france.avif" alt="fr-flag">
            </div>
            <div v-else-if="movieInfo.original_language === 'it'">
                <img src="../assets/img/flag-italy.png" alt="it-flag">
            </div>
            <div v-else-if="movieInfo.original_language === 'es'">
                <img src="../assets/img/flag-spain.png" alt="es-flag">
            </div>
            <div v-else>{{ movieInfo.original_language }}</div>

            <div>{{ movieInfo.vote_average }}</div>
        </div>
        <div class="ms-img">
            <img :src="'https://image.tmdb.org/t/p/w185' + movieInfo.poster_path" :alt="movieInfo.title">
        </div>
    </div>

</template>

<style scoped lang="scss">
.ms-infos {
    img {
        max-width: 10%;
    }
}
</style>