<template>
     <v-layout row wrap>
        <Recipe v-for="recipe in recipes" :key="recipe.id" :recipe="recipe"></Recipe>
     </v-layout>
 </template>
 <style>
</style>
<script>
import Recipe from './recipe-card.vue'
import RecipeService from '@/services/RecipeService'

export default {
  name: 'Recipes',
  data () {
    return {
      recipes: []
    }
  },
  async created () {
    this.Recipes()
  },
  mounted () {
    this.$root.$on('updateRecipes', (text) => {
      console.log('from recipes')
      console.log(text)
      this.Recipes()
    })
  },
  methods: {
    async Recipes () {
      let response = await RecipeService.getAll()
      this.recipes = response.data.recipes
    }
  },
  components: {
    Recipe
  }
}
</script>
