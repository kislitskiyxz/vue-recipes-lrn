<template>
  <div class="recipe">
    <div class="recipe__header">
      <h3 class="recipe__title">{{ name }}</h3>
      <div>
        <button
            class="btn btn--primary mr-1"
            @click="onSelect"
        >Edit
        </button>
        <button
            class="btn btn--danger"
            @click="onDelete"
        >Delete
        </button>
      </div>
    </div>
    <div class="recipe__row">
      <span class="recipe__label">Cook time:</span>
      <span class="recipe__value">{{ cookTime }}</span>
    </div>
    <div class="recipe__row">
      <span class="recipe__label">Servings:</span>
      <span class="recipe__value">{{ servings }}</span>
    </div>
    <div class="recipe__row">
      <span class="recipe__label">Instructions:</span>
      <div class="recipe__value recipe__instructions recipe__value--indented">{{ instructions }}</div>
    </div>
        <div class="recipe__row">
          <span class="recipe__label">Ingredients:</span>
          <div class="recipe__value recipe__value--indented">
            <IngredientList
              v-bind:list="ingredients"
            />
          </div>
        </div>
  </div>
</template>

<script>
import IngredientList from "../IngredientList";

export default {
  name: "Recipe",
  components: {
    IngredientList,
  },
  mounted() {
    console.log(this.ingredients)
  },
  props: {
    id: [Number, String],
    name: String,
    cookTime: String,
    servings: [String, Number],
    instructions: String,
    ingredients: Array,
    onDelete: Function,
    onSelect: Function,
  },
}
</script>

<style scoped>
</style>
