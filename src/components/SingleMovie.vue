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

            <span v-for="star in 5">
                <i v-if="star <= voteStars(movieInfo.vote_average)" class="fa-solid fa-star plain"></i>
                <i v-else class="fa-solid fa-star empty"></i>
            </span>
        </div>
        <div class="ms-img" v-if="movieInfo.poster_path">
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

.plain {
    color: rgb(236, 236, 21);
}

.empty {
    color: rgb(104, 103, 103);
}
</style>