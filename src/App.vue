<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="3">
        <v-text-field @input="changeChildFontSize"  v-model="fontSize" label="Размер шрифта (px)" type="number" min="8" max="100"></v-text-field>
      </v-col>
    </v-row>

    <TagsList :tags="tags" alignment="left" :fontSize="fontSize"/>
    <TagsList :tags="tags" alignment="justify" :fontSize="fontSize" />
    <div style="width: 50%">
      <TagsList :tags="tags" alignment="left" :fontSize="fontSize" />
    </div>
    <div style="width: 50%">
      <TagsList :tags="tags" alignment="justify" :fontSize="fontSize" />
    </div>
  </v-container>
</template>

<script>
// import { ref } from 'vue';
import TagsList from './components/TagsList.vue';

export default {
  name: 'App',
  components: {
    TagsList
  },
  data() {
    return {
      tags: [
        { text: "текст1" },
        { text: "текст2", icon: "mdi-star" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-access-point" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-star" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-star" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-access-point" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-star" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-star" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-access-point" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-star" },
        { text: "текст1" },
        { text: "текст2", icon: "mdi-star" },
      ],
      fontSize: 16,
    };
  },
  methods: {
    updateVisibleTags(){
      this.$refs.tagsList.updateVisibleTags();
    }
  }
};
</script>