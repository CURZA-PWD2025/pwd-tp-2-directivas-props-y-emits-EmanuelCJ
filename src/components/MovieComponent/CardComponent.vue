<template>
  <div class="container">
    <div v-for="movie in cantidad" :key="movie.id" class="card image-container ">
      <h2 class="card-title">{{ movie.titulo }}</h2>
      <img :src="movie.portada" alt="Movie Poster" class="card-image" />
      <div class="card-content">
        <p class="card-description"><strong>Estreno:</strong> {{ movie.anio }}</p>
        <p class="card-description"><strong>Género:</strong> {{ movie.generos }}</p>
        <p class="card-description"><strong>Director: </strong>{{ movie.director }}</p>
      </div>
      <div class="card-likes">
        <p><strong>LIKES:</strong> {{ movie.likes }}</p>
        <button v-if="turno" @click="Like(movie.id)"><img src="../MovieComponent/img/like.png" alt=""></button>
        <button v-else="turno" @click="desLike(movie.id)"><img src="../MovieComponent/img/deslike.png" alt=""></button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue';
import movies from '../MovieComponent/movies.ts';

const cantidad = reactive(movies);
const turno = ref(true); // Cambia a false para ocultar el botón de like

// Método para cambiar la imagen
const Like = (id: number) => {
  cantidad.forEach((movie) => {
    if (movie.id == id) {
      movie.likes++;
      turno.value = false; // Cambia el estado del botón a "deslike"
    }
  });
};
const desLike = (id: number) => {
  cantidad.forEach((movie) => {
    if (movie.id == id) {
      movie.likes--;
      turno.value = true; 
    }
  });
};

</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
}

.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  gap: 20px 20px;
}

.card {
  border: 1px solid #ccc;
  background-color: navy;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 16px;
  text-align: center;
  object-fit: cover;
}

.card-title {
  font-size: 1.5em;
  margin-bottom: 8px;
}

.card-image {
  width: 100%;
  height: auto;
  border-radius: 8px;

}

.card-likes img {
  width: 25px;
  height: 25px;
  margin: 0 5px;
}

.image-container img {
  max-width: 300px;
  object-fit: cover;
  /* Ajusta el contenido sin distorsión */
}
@media (max-width: 1000px) {
  .image-container img {
    /* Cambia el tamaño máximo para pantallas pequeñas */
    min-width: 200px;
  }

  .container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 10px 10px;
  }
  
}
@media (max-width: 600px) {
  .image-container img {
    /* Cambia el tamaño máximo para pantallas pequeñas */
    min-width: 200px;
  }

  .container {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr;
    gap: 10px 10px;
  }
}

.card-content {
  margin-top: 8px;
}
</style>