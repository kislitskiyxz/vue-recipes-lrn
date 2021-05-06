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
    servings: Number,
    instructions: String,
    ingredients: Array,
    onDelete: Function,
    onSelect: Function,
  },
}
</script>

<style scoped>
  .recipe {
    padding: 20px 20px 40px;
    border-bottom: 1px solid black;
  }
  .recipe:last-child {
    border-bottom: none;
    padding-bottom: 10px;
  }
  .recipe__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 25px;
  }
  .recipe__title {
    margin: 0;
    font-size: 1.2rem;
  }
  .recipe__row {
    margin-top: 10px;
  }
  .recipe__label {
    margin-right: 5px;
  }
  .recipe__value {
    font-weight: 300;
  }
  .recipe__value--indented {
    margin-top: 10px;
    margin-left: 20px;
  }
  .recipe__instructions {
    white-space: pre-wrap;
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
  .btn--primary:hover {
    background-color: hsl(200, 100%, 40%);
  }
  .btn--danger {
    color: white;
    background-color: hsl(0, 100%, 50%);
  }
  .btn--danger:hover {
    background-color: hsl(0, 100%, 40%);
  }
</style>
