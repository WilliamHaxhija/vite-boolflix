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
    }
}

</script>

<template>

<div class="col-3">
        <div class="card">
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
            
            <div>{{ tvSerieInfo.vote_average }}</div>
        </div>
    </div>

</template>

<style scoped lang="scss">

img {
        max-width: 10%;
    }

</style>