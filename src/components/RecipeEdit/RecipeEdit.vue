<template>
  <div>
    <span/>
    <div class="recipe-edit">
      <div class="recipe-edit__remove-button-container">
        <button
          class="btn recipe-edit__remove-button"
          @click="handleEditClose"
        >&times;</button>
      </div>

      <div class="recipe-edit__details-grid">
        <label for="name" class="recipe-edit__label">Name:</label>
        <input
          type="text"
          name="name"
          id="name"
          class="recipe-edit__input"
          v-model="localName"
        />

        <label for="cookTime" class="recipe-edit__label">Cook Time:</label>
        <input
          type="text"
          name="cookTime"
          id="cookTime"
          class="recipe-edit__input"
          v-model="localCookTime"
        />

        <label for="servings" class="recipe-edit__label">Servings:</label>
        <input
          type="number"
          min="1"
          name="servings"
          id="servings"
          class="recipe-edit__input"
          v-model="localServings"
        />

        <label for="instructions" class="recipe-edit__label">Instructions:</label>
        <textarea
          name="instructions"
          id="instructions"
          class="recipe-edit__input"
          v-model="localInstructions"
        />
      </div>
      <br />
      <label class="recipe-edit__label">Ingredients</label>
          <div class="recipe-edit__ingredient-grid">
            <div>Name</div>
            <div>Amount</div>
            <div></div>
            <RecipeIngredientsEdit
              v-for="ingredient in recipe.ingredients"
              :key="ingredient.id"
              v-bind="ingredient"
              :handleChange="handleIngredientChange"
              :handleRemove="removeIngredient"
            />
          </div>
          <div class="recipe-edit__add-ingredient-btn-container">
            <button
              class="btn btn--primary"
              @click="addNewIngredient"
            >Add Ingredient</button>
          </div>
    </div>
  </div>
</template>

<script>
import RecipeIngredientsEdit from "../RecipeIngredientsEdit";
import {v4 as uuidv4} from 'uuid'

export default {
  name: "RecipeEdit",
  components: {
    RecipeIngredientsEdit
  },
  props: {
    handleEditClose: Function,
    handleEditInput: Function,
    handleEditIngredient: Function,
    recipe: Object,
  },
  data(){
    return {
      localName: this.recipe.name,
      localCookTime: this.recipe.cookTime,
      localServings: this.recipe.servings,
      localInstructions: this.recipe.instructions
    }
  },
  watch: {
    localName(value){
      this.handleEditInput({name: value})
    },
    localCookTime(value){
      this.handleEditInput({cookTime: value})
    },
    localServings(value){
      this.handleEditInput({servings: value})
    },
    localInstructions(value){
      this.handleEditInput({instructions: value})
    },
  },
  methods: {
    handleIngredientChange(id, value){
      const index = this.recipe.ingredients.findIndex(ingredient => ingredient.id === id)
      this.handleEditIngredient(index, value)
    },
    addNewIngredient(){
      const newIngredient = {id: uuidv4(), name: '', amount: ''}
      this.$set( this.recipe.ingredients, this.recipe.ingredients.length, newIngredient)
    },
    removeIngredient(id){
      this.recipe.ingredients = this.recipe.ingredients.filter(i => i.id !== id)
    }
  }
}
</script>

<style scoped>
.recipe-edit {
  padding: 10px 30px 30px;
  position: sticky;
  right: 0;
  top: 0;
  width: calc(100% - 60px);
  max-height: 100%;
  overflow-y: auto;
}
.recipe-edit__remove-button-container {
  text-align: end;
}
.recipe-edit__remove-button {
  padding: 0;
  background: none;
  outline: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}
.recipe-edit__details-grid {
  display: grid;
  grid-template-columns: auto 1fr;
  row-gap: 10px;
  column-gap: 40px;
}
.recipe-edit__label {
  font-weight: bold;
}
.recipe-edit__input {
  border: 1px solid black;
  border-radius: 5px;
  font-size: inherit;
  padding: 5px 10px;
  outline: none;
  /*width: 100%;*/
}
textarea.recipe-edit__input {
  resize: none;
  height: 200px;
}
.recipe-edit__ingredient-grid {
  display: grid;
  grid-template-columns: repeat(3, auto);
  gap: 10px;
  margin-top: 20px;
  margin-left: 40px;
}
.recipe-edit__add-ingredient-btn-container {
  margin-top: 20px;
  text-align: center;
}
@media (max-width: 1000px) {
  .recipe-edit__details-grid,
  .recipe-edit__ingredient-grid {
    grid-template-columns: 1fr;
  }
}
</style>