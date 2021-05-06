<template>
  <div>
    <Ingredient
      v-for="ingredient in list"
      :key="ingredient.id"
      v-bind="ingredient"
    />
  </div>
</template>

<script>
import Ingredient from '../Ingredient'

export default {
  name: "IngredientList",
  components: {
    Ingredient
  },
  props: {
    list: Array,
    // id: String,
    // name: String,
    // amount: Number,
  }
}
</script>

<style scoped>
</style>