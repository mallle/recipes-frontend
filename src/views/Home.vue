<template>
  <div class="home">
    <div class="container">
      <div class="section">
        <h1 class="title is-1">Finde dein Rezept</h1>
      </div>
      <div class="section">
        <div class="columns is-multiline">
          <div class="column is-4" v-for="(recipe,index) in recipes" :key="index" >
            <RecipeCard  :id="recipe.id" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import RecipeCard from '@/components/RecipeCard.vue'

import axios from 'axios'
import { uri } from '../config'

export default {
  name: 'home',
  components: {
    RecipeCard
  },
  data() {
    return {
      recipes: null,
      tags: null
    }
  },
  mounted() {

    this.getAllRecipes();
    this.getAllTags();

  },
  methods: {
    getAllRecipes()
    {
      axios
        .get(`${uri}recipes`)
        .then(r => (this.recipes = r.data.data));
    },
    getAllTags()
    {
      axios
        .get(uri + 'tags')
        .then(response => {
          this.tags = response.data.data;
        })
        .catch(error => {
          console.log(error.response)
        });
    },
      getRequestedResipes(data) {
        axios
          .get(uri + 'tags/' +  data.tagId + '/recipes')
          .then(response => {
            this.recipes = response.data.data;
          })
          .catch(error => {
            console.log(error.response)
          });
      }
  }


}
</script>
