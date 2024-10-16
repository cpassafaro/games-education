<template>
  <v-container>
    <h2>Alphabetical Sortable</h2>
    <draggable v-model="words" group="people" item-key="id">
      <template #item="{ element }">
        <v-row>
          {{ element }}
        </v-row>
      </template>
    </draggable>
    <!-- <draggable v-model="words" v-bind="dragOptions" @change="onDragChange">
      <v-container
        class="justify-center align-center"
        v-for="index in words.length"
        :key="'sortable_' + index"
        >{{ words[index] }}</v-container
      >
    </draggable> -->
  </v-container>
</template>
<script>
import axios from "axios";
import draggable from "vuedraggable";

export default {
  name: "Sorting",
  components: { draggable },
  data() {
    return {
      sortingLength: 10,
      words: [],
    };
  },
  computed: {
    dragOptions() {
      return {
        animation: 200,
      };
    },
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
    onDragChange() {
      console.log("on drag change");
    },
  },
};
</script>
