
<template>
    <div class="container">
        <CardComponent v-for="movie in movies" :key="movie.id" :peliculas="movie" @eleccion="padreEscuchando" />
    </div>
</template>

<script setup lang="ts">

import CardComponent from './components/MovieComponent/CardComponent.vue';
import movies from '../src/components/MovieComponent/movies.ts';

function padreEscuchando(eleccion: string, id: number) {
    console.log('padre escuchando', eleccion, id);
    movies.forEach(element => {
        if (element.id === id) {
            if (eleccion === 'like') {
                console.log('modificando id:', id, 'tipo:', eleccion);
            } else if (eleccion === 'deslike') {
                console.log('modificando id:', id, 'tipo:', eleccion);
            }
        }
    });
}

</script>

<style scoped>
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 20px 20px;
}
@media screen and (max-width: 790px) and (min-width: 600px) {
    .container {
        grid-template-columns: 1fr 1fr;
        grid-template-rows: 1fr;
        gap: 10px 10px;
    }

}
@media screen and (max-width: 600px) {
    .container {
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 1fr;
        gap: 10px 10px;
    }

}
</style>