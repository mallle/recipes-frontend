<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <div class="container">
      <div class="columns is-multiline">
        <div class="column is-4" v-for="(recipe,index) in recipesFromHome" :key="index" >
          <RecipeCard  :id="recipe.id" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import RecipeCard from '@/components/RecipeCard.vue'

import axios from 'axios'

export default {
  name: 'home',
  components: {
    HelloWorld,
    RecipeCard
  },
  data() {
    return {
      recipesFromHome: null
    }
  },
  mounted () {
      axios
          .get('https://www.recipes.test/api/recipes')
          .then(r => (this.recipesFromHome = r.data.data));

  }


}
</script>
