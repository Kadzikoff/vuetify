<template>
    <v-list>
      <v-list-item-group v-model="selectedCategory">
        <v-list-item v-for="category in categories" :key="category" @click="selectCategory(category)" class="category-item">
          <v-list-item-content>
            <v-list-item-title>{{ category }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </template>
  
  <script>
  export default {
    props: {
      categories: Array
    },
    data() {
      return {
        selectedCategory: null
      };
    },
    methods: {
      selectCategory(category) {
        this.selectedCategory = category;
        this.$emit("category-click", category);
      }
    }
  };
  </script>
<style>
.v-list-item {
  cursor: pointer;
  margin: 10px;
  background-color: #FFFFFF;
}
</style>