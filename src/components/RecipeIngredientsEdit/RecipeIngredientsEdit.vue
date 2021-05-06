<template>
  <div>
    <input
      type="text"
      class="recipe-editinput"
      v-model="localName"
    />
    <input
      type="text"
      class="recipe-editinput"
      v-model="localAmount"
    />
    <button
      class="btn btn--danger"
      @click="() => handleRemove(id)"
    >&times;</button>
  </div>
</template>

<script>
export default {
  name: "RecipeIngredientsEdit",
  props: {
    id: [String, Number],
    name: String,
    amount: String,
    handleChange: Function,
    handleRemove: Function,
  },
  data(){
    return {
      localName: this.name,
      localAmount: this.amount,
    }
  },
  watch: {
    localName(value){
      this.handleChange(this.id, {
        id: this.id,
        name: value,
        amount: this.amount,
      })
    },
    localAmount(value){
      this.handleChange(this.id, {
        id: this.id,
        name: this.name,
        amount: value,
      })
    }
  }
  // data(){
  //   return {
  //     localName: this.name,
  //     localAmount: this.amount
  //   }
  // },
  // watch: {
  //   localName(value){this.handleChange(this.id, value)},
  //   localAmount(value){this.handleChange(this.id, value)},
  // }
}
</script>

<style scoped>

</style>