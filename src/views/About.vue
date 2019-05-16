<template>
  <div class="about">
    <pre>{{ recipes }}</pre>
  </div>
</template>



  <script>

  import axios from 'axios'
  import { uri } from '../config.js'

  export default {
    data(){
      return{
        recipes: []
      }
    },
    mounted() {
      axios.post(uri + 'tags/recipes', {
                name: "einfach",
              })
              .then(response => {
                this.recipes = response.data;
              })
              .catch(error => {
                  console.log(error.response)
              });

    },
  }
</script>s
