<template>
  <div class="ingredient-grid">
    <div>{{name}}</div>
    <div>{{amount}}</div>
  </div>
</template>

<script>
export default {
  name: "Ingredient",
  props: {
    id: [Number, String],
    name: String,
    amount: String,
  }
}
</script>

<style scoped>
.ingredient-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  column-gap: 40px;
  justify-content: flex-start;
}
.ingredient-grid + .ingredient-grid {
  margin-top: 5px;
}
</style>