<template>
    <v-form @submit.prevent="save">
      <v-text-field v-model="title" label="Название рецепта" required></v-text-field>
      <v-select v-model="category" :items="categories" label="Категория" required></v-select>
      <v-btn @click="addIngredient" color="success">Добавить ингредиент</v-btn>
      <v-row v-for="(ingredient, index) in ingredients" :key="index">
        <v-col>
          <v-text-field v-model="ingredients[index]" :label="'Ингредиент ' + (index + 1)" required></v-text-field>
        </v-col>
        <v-col>
          <v-btn @click="removeIngredient(index)" color="error" v-if="ingredients.length > 1">Удалить</v-btn>
        </v-col>
      </v-row>
      
      <v-btn @click="addStep" color="success" >Добавить шаг</v-btn>
      <v-row v-for="(step, index) in steps" :key="index">
        <v-col>
          <v-text-field v-model="steps[index]" :label="'Шаг ' + (index + 1)" required></v-text-field>
        </v-col>
        <v-col>
          <v-btn @click="removeStep(index)" color="error" v-if="steps.length > 1">Удалить</v-btn>
        </v-col>
      </v-row>
      

      <v-btn type="submit" color="primary">Сохранить</v-btn>
    </v-form>
</template>
  
<script>
  export default {
    props: {
      categories: Array
    },
    data() {
      return {
        title: "",
        category: "", 
        ingredients: [""],
        steps: [""]
      };
    },
    methods: {
      save() {
        const recipe = {
          title: this.title,
          category: this.category,
          ingredients: this.ingredients.filter(ingredient => ingredient.trim() !== ""),
          steps: this.steps.filter(step => step.trim() !== "")
        };
        this.$emit("save", recipe);
        this.resetForm();
      },
      resetForm() {
        this.title = "";
        this.category = ""; 
        this.ingredients = [""];
        this.steps = [""];
      },
      addIngredient() {
        this.ingredients.push("");
      },
      removeIngredient(index) {
        if (this.ingredients.length > 1) {
          this.ingredients.splice(index, 1);
        }
      },
      addStep() {
        this.steps.push("");
      },
      removeStep(index) {
        if (this.steps.length > 1) {
          this.steps.splice(index, 1);
        }
      }
    }
  };
</script>
<style>
v-dialog {
  display: flex;
  min-height: 0;
  flex-wrap: wrap;
  flex-direction: column;
  align-content: center;
  align-items: center;
}
</style>
  