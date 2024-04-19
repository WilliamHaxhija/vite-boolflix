<script>

import { store } from '../store.js';

export default {
    name: 'SingleCard',
    props: {
        cardInfo: Object
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
        <div class="ms-card overflow-y-auto mb-5" :class="{border: cardInfo.poster_path !== null}">
            
            <div class="ms-infos d-none p-4" :class="{dblock: cardInfo.poster_path === null}">
                <div><strong>Titolo:</strong> {{ cardInfo.title || cardInfo.name }}</div>
                <div v-if="cardInfo.original_title !== cardInfo.title || cardInfo.original_name !== cardInfo.name"><strong>Titolo Originale:</strong> {{ cardInfo.original_title || cardInfo.original_name }}</div>

                <div v-if="cardInfo.original_language === 'en'">
                    <img src="../assets/img/flag-uk.png" alt="en-flag">
                </div>
                <div v-else-if="cardInfo.original_language === 'fr'">
                    <img src="../assets/img/flag-france.avif" alt="fr-flag">
                </div>
                <div v-else-if="cardInfo.original_language === 'it'">
                    <img src="../assets/img/flag-italy.png" alt="it-flag">
                </div>
                <div v-else-if="cardInfo.original_language === 'es'">
                    <img src="../assets/img/flag-spain.png" alt="es-flag">
                </div>
                <div v-else><strong>Language:</strong> {{ cardInfo.original_language }}</div>

                <strong class="me-1">Voto:</strong>
                <span v-for="star in 5">
                    <i v-if="star <= voteStars(cardInfo.vote_average)" class="fa-solid fa-star plain"></i>
                    <i v-else class="fa-solid fa-star empty"></i>
                </span>

                <div v-if="cardInfo.overview"><strong>Overview:</strong> {{ cardInfo.overview }}</div>
            </div>

            <div class="ms-img" v-if="cardInfo.poster_path">
                <img :src="'https://image.tmdb.org/t/p/w342' + cardInfo.poster_path" :alt="cardInfo.title">
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