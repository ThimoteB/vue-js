<template>
  <div>
    <MovieSearch @searchMovieEmit="setMovieSearch"></MovieSearch>

    <MovieList
      @showMovieDetailEmit="showMovieDetail"
      :searchQuery="searchValue"
    />
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

export default {
  components: {
    MovieList,
    MovieDetail,
    MovieSearch,
  },
  data() {
    return {
      selectedMovie: null,
      dialog: false,
      searchValue: "",
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
    setMovieSearch(value) {
      this.searchValue = value;
    },
  },
};
</script>
