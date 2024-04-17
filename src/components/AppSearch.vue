<script>

import { store } from '../store.js';

    export default {
        name: 'AppSearch',

        data() {
            return {
               store
            };
        } 
    }

</script>

<template>

    <header>
        <div class="container-fluid d-flex py-3 justify-content-center">
            <input @keyup.enter="$emit('searchMovie')" v-model="store.searchedMovie" class="form-control me-3" type="text" placeholder="Search here...">
            <button @click="$emit('searchMovie')" type="button" class="btn btn-secondary">Search</button>
        </div>
    </header>

</template>

<style scoped lang="scss">

    input {
        max-width: 60%;
    }

</style>