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

    <div class="col-4 d-flex justify-content-center">
        <div class="ms-card overflow-y-auto border mb-5">
            <div class="ms-infos d-none p-4">
                <div><strong>Titolo:</strong> {{ tvSerieInfo.name }}</div>
                <div><strong>Titolo Originale:</strong> {{ tvSerieInfo.original_name }}</div>

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
                <div v-else><strong>Language:</strong> {{ tvSerieInfo.original_language }}</div>

                <strong class="me-1">Voto:</strong>
                <span v-for="star in 5">
                    <i v-if="star <= voteStars(tvSerieInfo.vote_average)" class="fa-solid fa-star plain"></i>
                    <i v-else class="fa-solid fa-star empty"></i>
                </span>
                <div v-if="tvSerieInfo.overview"><strong>Overview:</strong> {{ tvSerieInfo.overview }}</div>
            </div>
            <div class="ms-img" v-if="tvSerieInfo.poster_path">
                <img :src="'https://image.tmdb.org/t/p/w342' + tvSerieInfo.poster_path" :alt="tvSerieInfo.name">
            </div>
        </div>
    </div>

</template>

<style scoped lang="scss">

.ms-card {
    max-width: 345px;
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
    img {
        max-width: 10%;
    }

    > * {
        margin: 6px 0;
    }
}

.plain {
    color: rgb(236, 236, 21);
}

.empty {
    color: rgb(104, 103, 103);
}

</style>