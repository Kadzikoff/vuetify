<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col>
          <category-list :categories="categories" @category-click="showCategory" />
        </v-col>
        <v-col>
          <recipe-list :recipes="currentRecipes" @recipe-click="showRecipe" />
        </v-col>
        <v-col v-if="selectedRecipe">
          <recipe-details :recipe="selectedRecipe" />
        </v-col>
      </v-row>
      <v-dialog v-model="recipeEditorDialog" max-width="600">
        <v-card>
          <v-card-title>Добавить рецепт</v-card-title>
          <v-card-text>
            <recipe-editor :categories="categories" @save="saveRecipe" />
          </v-card-text>
          <v-card-actions>
            <v-btn @click="closeRecipeEditor">Закрыть</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-btn class="btn-position" @click="openRecipeEditor" color="primary">Добавить</v-btn>
    </v-container>
  </v-app>
</template>

<script>
import CategoryList from "@/components/CategoryList";
import RecipeList from "@/components/RecipeList";
import RecipeDetails from "@/components/RecipeDetails";
import RecipeEditor from "@/components/RecipeEditor";


export default {
  name: "App",
  data() {
    return {
      categories: ["Завтрак", "Обед", "Ужин"],
      recipes: [
        { id: 1, category: "Завтрак", title: "Омлет", ingredients: ["Яйца (2 шт).", "Молоко (250мл)", "Соль (1 чайная ложка)"], steps: ["Взбейте яйца", "Добавьте молоко и соль", "Жарьте на сковороде"] },
        { id: 2, category: "Обед", title: "Паста Болоньез", ingredients: ["Спагетти (200 гр.)", "Фарш говяжий (200 гр.)", "Лук (средний)", "Чеснок (2 зубчика)", "Томаты (черри, по желанию)"], steps: ["Обжарьте лук и чеснок", "Добавьте фарш и томаты", "Подавайте с спагетти"] },
        { id: 3, category: "Ужин", title: "Салат Цезарь", ingredients: ["Курица (500 гр.)", "Салат Айсберг (2 листа)", "Сухарики (2 пачки)", "Пармезан (150 гр.)", "Соус Цезарь"], steps: ["Обжарьте куриную грудку", "Смешайте все ингредиенты", "Полейте соусом"] }
      ],
      selectedCategory: null,
      selectedRecipe: null,
      recipeEditorDialog: false
    };
  },
  computed: {
    currentRecipes() {
      return this.selectedCategory
        ? this.recipes.filter(recipe => recipe.category === this.selectedCategory)
        : this.recipes;
    }
  },
  methods: {
    showCategory(category) {
      this.selectedCategory = category;
      this.selectedRecipe = null;
    },
    showRecipe(recipe) {
      this.selectedRecipe = recipe;
    },
    openRecipeEditor() {
      this.recipeEditorDialog = true;
    },
    closeRecipeEditor() {
      this.recipeEditorDialog = false;
    },
    saveRecipe(recipe) {
      // Добавляем новый рецепт в массив
      this.recipes.push(recipe);
      // Закрываем редактор
      this.closeRecipeEditor();
    }
  },
  components: {
    CategoryList,
    RecipeList,
    RecipeDetails
  },
    openRecipeEditor() {
      this.recipeEditorDialog = true;
    },
    closeRecipeEditor() {
      this.recipeEditorDialog = false;
    },
    saveRecipe(recipe) {
      // Добавляем новый рецепт в массив
      this.recipes.push(recipe);
      // Закрываем редактор
      this.closeRecipeEditor();
    },
    components: {
    CategoryList,
    RecipeList,
    RecipeDetails,
    RecipeEditor
  }
};
</script>
<style>
  .v-application__wrap {
    background-color: #4E598C;
  }
  .v-list {
    background-color: transparent;
  }
  .v-container {
    margin-top: 20px;
    display: flex;
    flex-direction: column;
  }

  .v-card {
    max-width: 400px;
    margin-top: 20px;
  }
  h1 {
    font-size: 50px;
    font-weight: bold;
    text-align: center;
    color: aliceblue;
  }
</style>