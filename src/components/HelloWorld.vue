<template>
  <v-container class="fill-height">
    <v-row>
      <v-app-bar>
        <v-row>
          <v-col cols="9">
            <h1 class="ml-6">Games</h1>
          </v-col>
          <v-col cols="3">
            <v-text-field
              hide-details
              variant="outlined"
              append-inner-icon="mdi-magnify"
            ></v-text-field>
          </v-col>
        </v-row>
      </v-app-bar>
    </v-row>
    <v-row class="row-selected-game">
      <!-- <DragAndDrop></DragAndDrop> -->
      <Sorting></Sorting>
    </v-row>
  </v-container>
</template>

<script>
import DragAndDrop from "./games/DragAndDrop.vue";
import Sorting from "./games/Sorting.vue";

export default {
  name: "HelloWorld",
  components: { DragAndDrop },
  props: {},
  data() {
    return {};
  },
  mounted() {},
  methods: {},
};
</script>
<style>
.row-selected-game {
  width: 100%;
}
</style>
