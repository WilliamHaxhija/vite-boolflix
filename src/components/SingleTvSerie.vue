<script>

import { store } from '../store.js';

export default {
    name: 'SingleTvSerie',
    props: {
        tvSerieInfo: Object
    },

    data() {
        return {
            store
        };
    },

    methods: {
        voteStars(number) {
            let integer = Math.round(number / 2);
            if (integer < 0) {
                return 1;
            } else if (integer > 5) {
                return 5;
            } else {
                return integer;
            };
        }
    }
}

</script>

<template>

    <div class="col-3">
        <div class="ms-infos">
            <div>{{ tvSerieInfo.name }}</div>
            <div>{{ tvSerieInfo.original_name }}</div>

            <div v-if="tvSerieInfo.original_language === 'en'">
                <img src="../assets/img/flag-uk.png" alt="en-flag">
            </div>
            <div v-else-if="tvSerieInfo.original_language === 'fr'">
                <img src="../assets/img/flag-france.avif" alt="fr-flag">
            </div>
            <div v-else-if="tvSerieInfo.original_language === 'it'">
                <img src="../assets/img/flag-italy.png" alt="it-flag">
            </div>
            <div v-else-if="tvSerieInfo.original_language === 'es'">
                <img src="../assets/img/flag-spain.png" alt="es-flag">
            </div>
            <div v-else>{{ tvSerieInfo.original_language }}</div>

            <div>{{ voteStars(tvSerieInfo.vote_average) }}</div>
        </div>
        <div class="ms-img" v-if="tvSerieInfo.poster_path">
            <img :src="'https://image.tmdb.org/t/p/w185' + tvSerieInfo.poster_path" :alt="tvSerieInfo.name">
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