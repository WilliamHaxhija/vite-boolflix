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

    <header class="fixed-top">
        <div class="container-fluid d-flex py-3 px-5 align-items-center">
            <h1 class="ms-5">BoolFlix</h1>
            <div class="d-flex flex-grow-1 justify-content-end me-5">
                <input @keyup.enter="$emit('searchContent')" v-model="store.searchedContent"
                    class="form-control me-3 p-2 h-25" type="text" placeholder="Search here...">
                <select class="form-select me-3">
                    <option selected>Open this select menu</option>
                    <option value="1">1</option>
                </select>
                <button @click="$emit('searchContent')" type="button" class="btn btn-secondary h-25">Search</button>
            </div>
        </div>
    </header>

</template>

<style scoped lang="scss">
header {
    background-color: black;
}

h1 {
    color: rgb(163, 8, 8);
}

input {
    max-width: 40%;
}

select {
    max-width: 15%;
}
</style>