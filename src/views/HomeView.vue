<template>
  <div>
    <MovieList @showMovieDetailEmit="showMovieDetail" />
    <v-dialog v-model="dialog" max-width="1200px">
      <MovieDetail
        v-if="selectedMovie"
        :movieId="selectedMovie"
        @closeDetail="closeDetail"
      />
    </v-dialog>
  </div>
</template>

<script>
import MovieDetail from "../components/MovieDetail.vue";
import MovieList from "../components/MovieList.vue";
import MovieSearch from "../components/movieSearch.vue";
import MoviePagination from "@/components/MoviePagination.vue";

export default {
  components: {
    MovieList,
    MovieDetail,
  },
  data() {
    return {
      selectedMovie: null,
      dialog: false,
    };
  },
  methods: {
    showMovieDetail(movie) {
      this.selectedMovie = movie.id;
      this.dialog = true;
    },
    closeDetail() {
      this.selectedMovie = null;
      this.dialog = false;
    },
  },
};
</script>
