<template>
  <div>
    <h2 class="card-title">{{ props.peliculas.titulo }}</h2>
    <img :src="props.peliculas.portada" alt="Movie Poster" class="card-image" />
    <div class="card-content">
      <p class="card-description"><strong>Estreno:</strong> {{ props.peliculas.anio }}</p>
      <p class="card-description"><strong>Género:</strong> {{ props.peliculas.generos }}</p>
      <p class="card-description"><strong>Director: </strong>{{ props.peliculas.director }}</p>
    </div>
    <div class="card-likes">
      <p><strong>LIKES:</strong> {{ likes }}</p>
      <button v-if="isDisabled" @click="UpdateLike('like', props.peliculas.id)">
        <img src="../MovieComponent/img/like.png" alt="like" class="img_btn" />
      </button>
      <button  v-else @click="UpdateLike('deslike', props.peliculas.id)">
        <img src="../MovieComponent/img/deslike.png" alt="deslike" class="img_btn" />
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits,ref } from 'vue';
import type { Pelicula } from '../../interfaces/Peliculas.ts';

const isDisabled = ref<boolean>(true);


// Definimos las props
const props = defineProps<{
  peliculas: Pelicula;
}>();

const likes = ref(props.peliculas.likes);

// Tipamos correctamente el emit con los argumentos que va a enviar
const emit = defineEmits<{
  (e: 'eleccion', tipo: string, id: number): void;
}>();

// Función que emite el evento
const UpdateLike = (tipo: string, id: number) => {
  emit('eleccion', tipo, id);
  if (tipo === 'like') {
    likes.value+=1;
    isDisabled.value = false; // Deshabilitar el botón después de hacer clic
  } else if (tipo === 'deslike') {
    likes.value-=1;
    isDisabled.value = true; 
  } 
};

</script>


<style scoped>
.card {
  background-color: #1e2a38;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.25);
  padding: 20px;
  text-align: center;
  color: #ffffff;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.35);
}

.card-title {
  font-size: clamp(1.5rem, 2.5vw, 2rem);
  margin-bottom: 12px;
  color: #00bcd4;
}

.card-image {
  width: 100%;
  height: 600px;
  object-fit: cover;
  border-radius: 10px;
  margin-bottom: 12px;
}

.card-content {
  margin-top: 8px;
}

.card-description {
  font-size: clamp(0.95rem, 2vw, 1.1rem);
  margin: 6px 0;
}

.card-likes {
  margin-top: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.card-likes p {
  font-weight: bold;
  margin-right: 10px;
  color: #fdd835;
}

.card-likes img {
  width: 30px;
  height: 30px;
  cursor: pointer;
  transition: transform 0.2s ease;
}

.card-likes img:hover {
  transform: scale(1.15);
}

/* Responsive extra pequeño */
@media (max-width: 480px) {
  .card {
    padding: 16px;
  }

  .card-image {
    height: 220px;
  }

  .card-title {
    font-size: 1.4rem;
  }
}


</style>