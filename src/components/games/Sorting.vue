<template>
  <v-container>
    <h2>Alphabetical Sortable</h2>
    <v-row>{{ this.words }}</v-row>
  </v-container>
</template>
<script>
import axios from "axios";

export default {
  name: "Sorting",
  data() {
    return {
      sortingLength: 10,
      words: [],
    };
  },
  mounted() {
    this.getWords();
  },
  methods: {
    getWords() {
      axios
        .get("https://random-word-api.herokuapp.com/word?number=10")
        .then((response) => (this.words = response.data));
    },
  },
};
</script>
