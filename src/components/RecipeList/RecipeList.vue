<template>
  <div class="recipe-list">
    <div>
      <Recipe
          v-for="recipe in list"
          :key="recipe.id"
          v-bind="recipe"
          :onDelete="() => handleRecipeDelete(recipe.id)"
          :onSelect="() => handleRecipeSelect(recipe.id)"
      />
    </div>
    <div class="recipe-list__add-recipe-btn-container">
      <button
          class="btn btn--primary"
          @click="handleRecipeAdd"
      >
        Add Recipe
      </button>
    </div>
  </div>
</template>


<script>
import Recipe from '../Recipe'

export default {
  name: "RecipeList",
  components: {
    Recipe,
  },
  props: {
    list: Array,
    handleRecipeDelete: Function,
    handleRecipeSelect: Function,
    handleRecipeAdd: Function,
  }
}
</script>


<style scoped>
  .recipe-list {
    border-right: 1px solid black;
    min-height: 100vh;
  }
  .recipe-list__add-recipe-btn-container {
    text-align: center;
    padding-top: 30px;
    padding-bottom: 30px;
  }
  .btn {
    background: none;
    font-size: inherit;
    font-weight: bold;
    border: none;
    outline: none;
    border-radius: 5px;
    padding: 5px 20px;
    cursor: pointer;
  }
  .btn--primary {
    color: white;
    background-color: hsl(200, 100%, 50%);
  }
</style>