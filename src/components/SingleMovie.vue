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

    <div class="col-4 d-flex justify-content-center">
        <div class="ms-card overflow-y-auto mb-5" :class="{border: movieInfo.poster_path !== null}">
            <div class="ms-infos d-none p-4" :class="{dblock: movieInfo.poster_path === null}">
                <div><strong>Titolo:</strong> {{ movieInfo.title }}</div>
                <div v-if="movieInfo.original_name !== movieInfo.name"><strong>Titolo Originale:</strong> {{ movieInfo.original_title }}</div>

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
                <div v-else><strong>Language:</strong> {{ movieInfo.original_language }}</div>

                <strong class="me-1">Voto:</strong>
                <span v-for="star in 5">
                    <i v-if="star <= voteStars(movieInfo.vote_average)" class="fa-solid fa-star plain"></i>
                    <i v-else class="fa-solid fa-star empty"></i>
                </span>

                <div v-if="movieInfo.overview"><strong>Overview:</strong> {{ movieInfo.overview }}</div>
            </div>
            <div class="ms-img" v-if="movieInfo.poster_path">
                <img :src="'https://image.tmdb.org/t/p/w342' + movieInfo.poster_path" :alt="movieInfo.title">
            </div>
        </div>
    </div>

</template>

<style scoped lang="scss">

.ms-card {
    width: fit-content;
    height: 515px;
    color: white;
    background-color: rgb(10, 10, 10);
    cursor: pointer;

    &:hover .ms-infos {
        display: block !important;
    }

    &:hover .ms-img {
        display: none;
    }
}

.ms-infos {
    height: 100%;
    min-width: 335px;
    img {
        max-width: 10%;
    }

    > * {
        margin: 6px 0;
    }
}

.ms-img {
    height: 100%;
    
    img{
        height: 100%;
        object-fit: cover;
    }

}

.plain {
    color: rgb(236, 236, 21);
}

.empty {
    color: rgb(104, 103, 103);
}

.dblock {
    display: block!important;
}

</style>