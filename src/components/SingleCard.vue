<script>

import axios from 'axios';
import { store } from '../store.js';

export default {
    name: 'SingleCard',
    props: {
        cardInfo: Object
    },

    data() {
        return {
            store,
            flags: [
                'en',
                'it',
                'fr',
                'es',
                'ja',
                'de'
            ],
            actorsList: [],
            contentGenres: []
        };
    },

    methods: {
        getFlagImageUrl() {
            let flagImgName = this.cardInfo.original_language + '.png';
            return new URL(`../assets/img/${flagImgName}`, import.meta.url).href;
        },
        voteStars(number) {
            let integer = Math.round(number / 2);
            if (integer < 0) {
                return 1;
            } else if (integer > 5) {
                return 5;
            } else {
                return integer;
            };
        },
        getContentActorsListFromApi() {
            let apiUrl = `https://api.themoviedb.org/3/movie/${this.cardInfo.id}/credits?api_key=25378c3a1e8ccece435091404e238d2c`;
            axios.get(apiUrl).then((response) => {
                this.actorsList = response.data.cast.slice(0, 5);
            });
        },
        getContentGenres() {
            store.genresList.forEach(genre => {
                if (this.cardInfo.genre_ids.includes(genre.id)) {
                    this.contentGenres.push(genre.name);
                }
            });
        }
    },
    mounted() {
        this.getContentGenres()
    }
}

</script>

<template>

    <div v-if="contentGenres.includes(store.selectedGenre) || store.selectedGenre === 'Scegli un genere' || store.selectedGenre === ''"
        class="col-4 d-flex justify-content-center">
        <div class="ms-card overflow-y-auto mb-5" :class="{ border: cardInfo.poster_path !== null }"
            @mouseenter="getContentActorsListFromApi()">

            <div class="ms-infos d-none p-4" :class="{ dblock: cardInfo.poster_path === null }">

                <div><strong>Title:</strong> {{ cardInfo.title || cardInfo.name }}</div>

                <div v-if="cardInfo.original_title !== cardInfo.title || cardInfo.original_name !== cardInfo.name">
                    <strong>Original Title:</strong> {{ cardInfo.original_title || cardInfo.original_name }}
                </div>

                <div>
                    <img v-if="flags.includes(cardInfo.original_language)" :src="getFlagImageUrl()"
                        :alt="cardInfo.original_language">
                    <span v-else><strong class="me-1">Language:</strong> {{ cardInfo.original_language }}</span>
                </div>

                <strong class="me-1">Vote:</strong>
                <span v-for="star in 5">
                    <i v-if="star <= voteStars(cardInfo.vote_average)" class="fa-solid fa-star plain"></i>
                    <i v-else class="fa-solid fa-star empty"></i>
                </span>

                <div v-if="cardInfo.overview"><strong>Overview:</strong> {{ cardInfo.overview }}</div>

                <div v-if="actorsList.length > 0">
                    <span><strong>Actors</strong></span>
                    <div v-for="actor in actorsList">{{ actor.name }} - {{ actor.character }}</div>
                </div>

                <div class="pb-5" v-if="contentGenres.length > 0">
                    <span><strong>Genres</strong></span>
                    <div>{{ contentGenres.join(', ') }}</div>
                </div>

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

    >* {
        margin: 6px 0;
    }
}

.ms-img {
    height: 100%;

    img {
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
    display: block !important;
}
</style>