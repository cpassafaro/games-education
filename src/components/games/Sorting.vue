<template>
  <v-row>
    <v-col cols="12" class="d-flex justify-center">
      <h2>Alphabetical Sortable</h2>
    </v-col>
    <v-col v-if="loading" class="d-flex justify-center">
      <v-progress-circular
        :size="70"
        :width="7"
        indeterminate
        color="purple"
      ></v-progress-circular>
    </v-col>
    <v-col v-else cols="12" class="d-flex justify-center">
      <draggable v-model="words" group="people" item-key="id">
        <template #item="{ element }">
          <v-row class="outlined  pa-4">
            {{ element.word[0] }}
          </v-row>
        </template>
      </draggable>
    </v-col>
  </v-row>
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
      loading: true,
    };
  },
  computed: {
    dragOptions() {
      return {
        animation: 200,
      };
    },
  },
  watch: {
    words(newValue) {
      console.log("words ", newValue);
    },
  },
  mounted() {
    this.getWords();
  },
  methods: {
    async getWords() {
      for (let i = 0; i < 10; i++) {
        // https://api-ninjas.com/api/randomword
        axios.defaults.headers.common = {
          "X-API-Key": "PanCkRPVcOtni+YlYusDwg==dmIM4Ykz0odODuwA",
        };

        await axios
          .get("https://api.api-ninjas.com/v1/randomword")
          .then((response) => this.words.push(response.data));
      }
      this.loading = false;
    },
    onDragChange() {
      console.log("on drag change");
    },
  },
};
</script>
<style>
.row-header {
  width: 100%;
}
.row-draggable {
  width: 100%;
}
.container-row-word {}
</style>
