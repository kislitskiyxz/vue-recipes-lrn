<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div v-for="(name, index) in getNames()" v-bind:key="index">{{name}}</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
    sampleRecipes: [
      {
        id: 1,
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
        id: 2,
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
  }),
  props: {
    msg: String
  },
  methods: {
    getNames(){
      console.log(this.sampleRecipes)
      return this.sampleRecipes.map(recipe => recipe.name)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
