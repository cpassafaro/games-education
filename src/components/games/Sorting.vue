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
      for (let i = 0; i < 10; i++) {
        // https://api-ninjas.com/api/randomword
        axios.defaults.headers.common = {
          "X-API-Key": "PanCkRPVcOtni+YlYusDwg==dmIM4Ykz0odODuwA",
        };

        axios
          .get("https://api.api-ninjas.com/v1/randomword")
          .then((response) => this.words.push(response.data));
      }
    },
    onDragChange() {
      console.log("on drag change");
    },
  },
};
</script>
