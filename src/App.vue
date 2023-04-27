<script setup>
import { reactive } from "vue";
import { StarIcon } from "@heroicons/vue/24/solid";
import { items } from "./movies.json";
const movies = reactive(items);

const updateRating = (id, star) => {
  movies.forEach((movie) => {
    if (movie.id === id) {
      movie.rating = star;
    }
  });
};
</script>

<template>
  <div class="app">
    <div class="movie-list">
      <div class="movie-item" v-for="movie in movies" :key="movie.id">
        <div class="movie-item-image-wrapper">
          <img :src="movie.image" class="movie-item-image" alt="" />
        </div>

        <div class="movie-item-content-wrapper">
          <div class="movie-item-title-wrapper">
            <h3 class="movie-item-title">{{ movie.name }}</h3>
            <div class="movie-item-genres-wrapper">
              <span v-for="genre in movie.genres" :key="`${movie.id}-${genre}`" class="movie-item-genre-tag">{{ genre
              }}</span>
            </div>
          </div>
          <div class="movie-item-description-wrapper">
            <p class="movie-item-description">{{ movie.description }}</p>
          </div>
          <div class="movie-item-rating-wrapper">
            <span class="movie-item-rating-text">
              Rating: ({{ movie.rating }}/5)
            </span>
            <template v-for="star in movie.rating" :key="`star-${star}`">
              <button :disabled="movie.rating == star" @click="updateRating(movie.id, star)">
                <StarIcon class="movie-item-star-icon" />
              </button>
            </template>
            <button v-for="star in 5 - movie.rating" :key="`star-${star}`"
              @click="updateRating(movie.id, star + movie.rating)">
              <StarIcon class="movie-item-star-icon-gray" />
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
