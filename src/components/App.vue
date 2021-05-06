<template>
  <div class="main-app">
    <RecipeList
      :list="recipes"
      :handleRecipeDelete="handleRecipeDelete"
      :handleRecipeSelect="handleRecipeSelect"
      :handleRecipeAdd="handleRecipeAdd"
    />
    <RecipeEdit
      :key="currentRecipeId"
      v-if="currentRecipeId !== null"
      :handleEditClose="handleEditClose"
      :handleEditInput="handleEditInput"
      :recipe="getCurrentRecipe()"
    />
    <div>{{currentRecipeId}}</div>
  </div>
</template>

<script>
import RecipeList from './RecipeList'
import RecipeEdit from "./RecipeEdit";
import {v4 as uuidv4} from 'uuid'

const mockRecipes = [
  {
    id: '1',
    name: "Plain Chicken",
    cookTime: "1.54",
    servings: 3,
    instructions: "1. Put salt on chicken\n" +
      "2. Put chicken in the oven\n" +
      "3. Eat chicken",
    ingredients: [
      {
        id: 1,
        name: "Chicken",
        amount: "2 Pounds"
      },
      {
        id: 2,
        name: "Salt",
        amount: "1 Tbs"
      }
    ]
  },
  {
    id: '2',
    name: "Plain Pork",
    cookTime: "0.54",
    servings: 5,
    instructions: "1. Put paprika on pork\n" +
      "2. Put pork in the oven\n" +
      "3. Eat pork",
    ingredients: [
      {
        id: 1,
        name: "Pork",
        amount: "3 Pounds"
      },
      {
        id: 2,
        name: "Paprika",
        amount: "2 Tbs"
      }
    ]
  }
]
const writeRecipeListToLS = (value) => {
  localStorage.setItem('recipe_list', JSON.stringify(value))
}

export default {
  name: 'App',
  components: {
    RecipeList,
    RecipeEdit
  },
  mounted() {
    let list = JSON.parse(localStorage.getItem('recipe_list'))
    if (!list) {
      writeRecipeListToLS(mockRecipes)
      list = mockRecipes
    }
    this.recipes = list
  },
  data: () => ({
    recipes: [],
    currentRecipeId: null,
  }),
  methods: {
    handleRecipeDelete(id) {
      this.currentRecipeId = null
      const filteredList = this.recipes.filter(recipe => recipe.id !== id)
      this.recipes = filteredList
      writeRecipeListToLS(filteredList)
    },
    handleRecipeSelect(id) {
      this.currentRecipeId = id
    },
    handleRecipeAdd() {
      const newList = [
        ...this.recipes,
        {
          id: uuidv4(),
          name: '',
          cookTime: '',
          servings: 1,
          instructions: '',
          ingredients: [],
        }
      ]
      this.recipes = newList
      writeRecipeListToLS(newList)
    },
    handleEditClose() {
      this.currentRecipeId = null
      writeRecipeListToLS(this.recipes)
    },
    getCurrentRecipe() {
      return this.recipes.find(recipe => recipe.id === this.currentRecipeId)
    },
    handleEditInput(change) {
      const index = this.recipes.findIndex(recipe => recipe.id === this.currentRecipeId)
      this.$set(this.recipes, index, {...this.recipes[index], ...change})
    }
  }
}
</script>

<style>
.main-app {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
}
</style>
