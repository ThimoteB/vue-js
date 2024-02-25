<template>
  <v-card v-if="movie">
    <v-img
      :src="`${config.url.photo_path}${movie.backdrop_path}`"
      aspect-ratio="1.5"
    ></v-img>
    <v-card-title>{{ movie.title }}</v-card-title>
    <v-card-subtitle>
      <v-chip color="primary" text-color="white">
        <v-avatar left>
          <v-icon>mdi-star</v-icon>
        </v-avatar>
        {{ movie.vote_average }}
        <span
          v-for="star in parseInt(movie.vote_average)"
          :key="star"
          class="star"
        >
          <v-icon color="amber darken-3">mdi-star</v-icon>
        </span>
      </v-chip>
    </v-card-subtitle>
    <v-card-text>{{ movie.overview }}</v-card-text>
    <v-card-actions class="justify-center">
      <v-btn color="primary" @click="closeDetail">Fermer</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import axios from "axios";
import config from "@/config.json";

export default {
  props: {
    movieId: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      config,
      movie: null,
    };
  },
  watch: {
    movieId(newMovieId) {
      this.fetchMovie(newMovieId);
    },
  },
  created() {
    this.fetchMovie(this.movieId);
  },
  methods: {
    fetchMovie(movieId) {
      axios
        .get(
          `${config.url.movie_detail}${movieId}?api_key=${config.api_key}&language=fr-FR`
        )
        .then((response) => {
          this.movie = response.data;
          console.log(this.movie);
        })
        .catch((error) => {
          console.error(error);
        });
    },
    closeDetail() {
      this.$emit("closeDetail");
    },
  },
};
</script>
