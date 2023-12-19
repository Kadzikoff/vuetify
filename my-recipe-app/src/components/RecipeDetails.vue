<template>
    <v-card>
      <v-card-title>{{ recipe.title }}</v-card-title>
      <v-card-subtitle>{{ recipe.category }}</v-card-subtitle>
      <v-card-text class="v-card-text">
        <v-list>
          <v-list-item-group>
            <v-list-item class="v-list-item2">
              <v-list-item-content>
                <v-list-item-title class="subtitle, v-list-item-content2">Ингредиенты:</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-list-item class="v-list-item2" v-for="(ingredient, index) in recipe.ingredients" :key="index">
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon>mdi-minus</v-icon>{{ ingredient }}
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
        <v-divider></v-divider>
        <v-list>
          <v-list-item-group>
            <v-list-item class="v-list-item2">
              <v-list-item-content>
                <v-list-item-title  class="subtitle, v-list-item-content2">Рецепт:</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-list-item class="v-list-item2" v-for="(step, index) in recipe.steps" :key="index">
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon>mdi-numeric-{{ index + 1 }}</v-icon>{{ step }}
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card-text>
    </v-card>
  </template>
  
  <script>
  export default {
    props: {
      recipe: Object
    }
  };
  </script>
  
  <style>
  .v-card {
    width: 400px;
    background-color: #F9C784;
  }

  .v-card-title {
    font-size: 30px;
    font-weight: bold;
    background-color: #FCAF58;

  }

  .v-card-subtitle {
    font-size: 20px;
    color: rgb(73, 73, 73);
    background-color: #FCAF58;
    
  }

  .v-list-item-title {
    font-size: 20px;
  }
  .v-list-item2{
    background-color: #F9C784;
  }
  .v-list-item-content2{
    font-weight: bold;
  }
</style>
  