<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <div class="container">
      <div class="section">
        <div class="buttons are-medium">
          <a  class="button" type="is-info" size="is-medium" @click="getAllRecipes">All</a>
          <a  class="button" v-for="(tag, index) in tags" :key="index" type="is-info" size="is-medium" @click="getRequestedResipes(tag.id)">{{ tag.name }}</a>
        </div>
      </div>

      <div class="columns is-multiline">
        <div class="column is-4" v-for="(recipe,index) in recipes" :key="index" >
          <RecipeCard  :id="recipe.id" />
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
      axios.get(uri + 'tags')
              .then(response => {
                this.tags = response.data.data;
              });
              // .catch(error => {
              //   //console.log(error.response)
              // });
    },
    getRequestedResipes(id) {
      axios.get(uri + 'tags/' +  id + '/recipes')
              .then(response => {
                this.recipes = response.data.data;
              });
              // .catch(error => {
              //   //console.log(error.response)
              // });
    }
  }


}
</script>
