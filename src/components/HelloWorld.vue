<template>
  <v-header> </v-header>
  <v-container class="fill-height">
    <v-row>
      <v-app-bar>
        <v-row>
          <v-col cols="9"></v-col>
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
    <v-row>
      <DragAndDrop></DragAndDrop>
    </v-row>
  </v-container>
</template>

<script>
import DragAndDrop from "./games/DragAndDrop.vue";
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
