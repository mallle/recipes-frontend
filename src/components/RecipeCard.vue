<template>
    <div class="card">
        <div class="card-image">
            <figure class="image is-4by3">
                <img :src="recipe.image" :alt="'Foto von ' + recipe.name">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-left">
                    <figure class="image is-48x48">
                        <img src="https://bulma.io/images/placeholders/96x96.png" alt="Placeholder image">
                    </figure>
                </div>
                <div class="media-content">
                    <router-link :to="`/recipe/${recipe.id}`" tag="p" class="title is-4">{{ recipe.name }}</router-link >
                    <p class="subtitle is-6">@johnsmith</p>
                </div>
            </div>

            <div class="content">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                Phasellus nec iaculis mauris. <a>@bulmaio</a>.
                <a href="#">#css</a> <a href="#">#responsive</a>
                <br>
                <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
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