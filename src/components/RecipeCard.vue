<template>
    <div class="card">
        <div class="card-image">
            <figure class="image is-4by3">
                <img :src="recipe.image" :alt="'Foto von ' + recipe.name">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <router-link :to="`/recipe/${recipe.id}`" tag="p" class="title is-4">{{ recipe.name }}</router-link >
                </div>
            </div>


            <div class="content">
                <b-taglist>
                    <b-tag v-for="(tag, index) in recipe.tags" :key="index" size="is-medium">{{ tag.name }}</b-tag>
                </b-taglist>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: "RecipeCard.vue",
        props: {
            id: Number
        },
        data(){
            return{
                recipe: []
            }
        },
        mounted() {
            axios
                  .get(`https://www.recipes.test/api/recipes/${this.id}`)
                  .then(r => (this.recipe = r.data.data));


        },


    }
</script>

<style scoped>

</style>