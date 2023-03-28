<template>
  <div>
    <h1>Random Recipe Generator</h1>
    <button @click="getRandomRecipe">Get a Recipe</button>
    <div v-if="recipe">
      <h2>{{ recipe.title }}</h2>
      <img :src="recipe.image" alt="recipe image">
      <p>{{ recipe.summary }}</p>
      <h3>Ingredients</h3>
      <ul>
        <li v-for="(ingredient, index) in recipe.ingredients" :key="index">{{ ingredient }}</li>
      </ul>
      <h3>Instructions</h3>
      <ol>
        <li v-for="(instruction, index) in recipe.analyzedInstructions" :key="index">
          <ol>
            <li v-for="(step, stepIndex) in instruction.steps" :key="stepIndex">{{ step.step }}</li>
          </ol>
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      recipe: null
    }
  },
  methods: {
    async getRandomRecipe() {
      try {
        const response = await fetch(`https://api.spoonacular.com/recipes/random?apiKey=93a4a41cb9ba4b6498079554ccabb21c&number=1`);
        const data = await response.json();
        this.recipe = data.recipes[0];
      } catch (error) {
        console.error(error);
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ol {
  text-align: left;
}
</style>