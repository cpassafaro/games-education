<template>
  <v-row>
    <v-col cols="12" class="d-flex justify-center">
      <h2>Alphabetical Sortable</h2>
    </v-col>
    <v-col cols="12" class="d-flex justify-center">
      <p>Drag the words into Alphabetical Order. Then submit below.</p>
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
          <v-card class="outlined pa-4 mb-4 row-word">
            <!-- <v-col class="pa-0" cols="3">
            </v-col> -->
            <v-icon>mdi-drag-vertical</v-icon>
            <!-- <v-col class="pa-0">
            </v-col> -->
            <span>
              {{ element.word[0] }}
            </span>
          </v-card>
        </template>
      </draggable>
    </v-col>
    <v-col cols="12" class="d-flex justify-center">
      <v-btn color="green" @click="onSubmit">Submit</v-btn>
    </v-col>
  </v-row>
</template>
<script>
import _ from "lodash";
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
      for (let i = 0; i < 5; i++) {
        // https://api-ninjas.com/api/randomword
        axios.defaults.headers.common = {
          "X-API-Key": "PanCkRPVcOtni+YlYusDwg==dmIM4Ykz0odODuwA",
        };

        await axios
          .get("https://api.api-ninjas.com/v1/randomword")
          .then((response) => this.words.push(response.data));
      }
      console.log(this.words);
      this.loading = false;
    },
    onDragChange() {
      console.log("on drag change");
    },
    onSubmit() {
      const cloneWords = _.cloneDeep(this.words);
      const sortedWords = cloneWords.sort((a, b) =>
        a.word[0].localeCompare(b.word[0])
      );
      // still need to compare and throw feedback
      console.log(sortedWords);
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
.container-row-word {
}
.row-word {
  width: 15vw;
}
.row-word:hover {
  cursor: grab;
}
</style>
