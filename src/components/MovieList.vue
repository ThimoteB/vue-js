<template>
  <div>
    <v-row>
      <v-col v-for="movie in movieFiltered" :key="movie.id" cols="3">
        <v-card>
          <v-img
            :src="`${config.url.photo_path}${movie.poster_path}`"
            height="300"
          ></v-img>
          <v-card-title class="text-h4" style="text-align: center">
            {{ movie.title }}
          </v-card-title>
          <v-card-subtitle style="text-align: center">
            {{ movie.overview ? movie.overview : "Pas d'info" }}
          </v-card-subtitle>
          <v-card-actions class="justify-center">
            <v-btn text color="primary" @click="sendMovie(movie)">
              Plus d'information
              <v-icon right>mdi-arrow-up</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from "axios";
import config from "@/config.json";

export default {
  name: "MoviesList",
  props: {
    searchQuery: String,
  },
  data() {
    return {
      config,
      movies: [],
    };
  },
  created() {
    this.fetchMovies();
  },
  methods: {
    async fetchMovies() {
      const url = `${config.url.movie_list}&api_key=${config.api_key}`;
      axios.get(url).then((response) => {
        this.movies = response.data.results;
      });
    },
    sendMovie(movie) {
      this.$emit("showMovieDetailEmit", movie);
    },
  },
  computed: {
    movieFiltered() {
      if (!this.searchQuery) return this.movies;
      return this.movies.filter((movie) => {
        return movie.title
          .toLowerCase()
          .includes(this.searchQuery.toLowerCase());
      });
    },
  },
};
</script>
