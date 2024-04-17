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
        <div class="card">
            <div>{{ movieInfo.title }}</div>
            <div>{{ movieInfo.original_title }}</div>
            <div>{{ movieInfo.original_language }}</div>
            <div>{{ movieInfo.vote_average }}</div>
        </div>
    </div>

</template>

<style scoped lang="scss"></style>