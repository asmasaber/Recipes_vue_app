<template>
     <v-layout row wrap>
        <Recipe v-for="recipe in recipes" :key="recipe.id" :recipe="recipe"></Recipe>
     </v-layout>
 </template>
 <style>
</style>
<script>
import Recipe from './recipe-card-actions.vue'
import RecipeService from '@/services/RecipeService'
import { mapState } from 'vuex'

export default {
  name: 'Recipes',
  data () {
    return {
      recipes: []
    }
  },
  async created () {
    // if (!this.isUserLoggedIn) {
    //   this.$router.push({ name: 'login' })
    // }
    this.Recipes()
  },
  mounted () {
    this.$root.$on('updateRecipes', (text) => {
      console.log('from user recipes')
      console.log(text)
      this.Recipes()
    })
  },
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user'
    ])
  },
  methods: {
    async Recipes () {
      let response = await RecipeService.getUserRecips()
      this.recipes = response.data.recipes
    }
  },
  components: {
    Recipe
  }
}
</script>
