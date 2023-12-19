<template>
    <v-list>
      <v-list-item-group v-model="selectedRecipe">
        <v-list-item v-for="recipe in recipes" :key="recipe.id" @click="selectRecipe(recipe)" class="recipe-item">
          <v-list-item-content>
            <v-list-item-title>{{ recipe.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </template>
  
  <script>
  export default {
    props: {
      recipes: Array
    },
    data() {
      return {
        selectedRecipe: null
      };
    },
    methods: {
      selectRecipe(recipe) {
        this.selectedRecipe = recipe;
        this.$emit("recipe-click", recipe);
      }
    }
  };
  </script>
<style>
.v-list-item {
  cursor: pointer;
}
</style>

  