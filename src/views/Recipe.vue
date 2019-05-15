<template>
    <div class="container">
        <figure class="image is-2by1">
            <img :src="recipe.image">
        </figure>

        <div class="section">
            <nav class="level">
                <div class="level-item has-text-centered">
                    <div>
                        <p class="heading">Preparation time</p>
                        <p class="title">{{recipe.preparationtime}}</p>
                    </div>
                </div>
                <div class="level-item has-text-centered">
                    <div>
                        <p class="heading">Resttime</p>
                        <p class="title">{{ recipe.resttime }}</p>
                    </div>
                </div>
                <div class="level-item has-text-centered">
                    <div>
                        <p class="heading">Baking time</p>
                        <p class="title">{{ recipe.bakingtime }}</p>
                    </div>
                </div>
                <div class="level-item has-text-centered">
                    <div>
                        <p class="heading">Effort</p>
                        <p class="title">{{ recipe.effort }}</p>
                    </div>
                </div>
            </nav>
        </div>

        <div class="section">
            <div class="columns">
                <div class="column is-5">

                        <b-icon
                                pack="fas"
                                icon="plus"
                                size="is-small">
                        </b-icon>
                        <span class="number-of-persons">{{recipe.persons}}</span>
                        <b-icon
                                pack="fas"
                                icon="minus"
                                size="is-small">
                        </b-icon>

                    <table class="table is-narrow">
                        <tbody>
                            <tr v-for="(ingredient, index) in recipe.ingredients" :key="index">
                                <td class="has-text-right">{{ingredient.amount }}<td>
                                <td>{{ingredient.type }} {{ingredient.name }}</td>
                            </tr>
                        </tbody>
                    </table>
                    <div class="block">
                        <b-taglist>
                            <b-tag v-for="(tag, index) in recipe.tags" :key="index" type="is-info" size="is-medium">{{ tag.name }}</b-tag>
                        </b-taglist>
                    </div>

                </div>
                <div class="column has-text-left">
                    <div class="content" v-for="step in recipe.descriptions" :key="step.id">
                        <div class="tags are-medium">
                            <span class="tag">{{step.descriptionnumber}}</span>

                        </div><hr>

                        <p class="description">{{step.description}}</p>
                    </div>
                </div>
            </div>
        </div>
        <pre>{{recipe}}</pre>
    </div>
</template>

<script>

    import axios from 'axios'

    export default {
        data(){
            return{
                recipe: []
            }
        },
        mounted() {
            axios
                .get(`https://www.recipes.test/api/recipes/${this.$route.params.id}`)
                .then(r => (this.recipe = r.data.data));

        },
    }
</script>

<style scoped>
    .number-of-persons{
        margin: 0 10px 0 10px;
        font-size: 1.5rem;
    }
    .table td, .table th {
        border-color: white;
    }

    hr{
        margin: -2.5rem 8rem 1rem 51px;
    }

    .description{
        padding-left: 3.3rem;
    }
</style>