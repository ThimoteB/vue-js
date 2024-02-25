<template>
  <v-text-field
    v-model="searchQuery"
    label="Rechercher un film"
    single-line
    clearable
  ></v-text-field>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
    };
  },
  watch: {
    searchQuery(newVal) {
      this.$emit("searchMovieEmit", newVal);
    },
  },
};
</script>
