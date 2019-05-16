<template>
    <div class="container">
        <figure class="image is-2by1">
            <img :src="recipe.image">
        </figure>

        <div class="section">
            <nav class="level">
                <div class="level-item">
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
                <div class="column">

                    <a class="button" @click="persons--">
                        <span class="icon is-small">
                          <i class="fas fa-minus"></i>
                        </span>
                    </a>

                        <span class="number-of-persons">{{persons}}</span>
                    <a class="button" @click="persons++">
                        <span class="icon is-small">
                          <i class="fas fa-plus"></i>
                        </span>
                    </a>

                    <table class="table is-narrow">
                        <tbody>
                            <tr v-for="(ingredient, index) in recipe.ingredients" :key="index">
                                <td class="has-text-right">{{ingredient.amount_per_person  * persons}}<td>
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
                <div class="column ">

                </div>

            </div>
        </div>
        <div class="section">
            <div class="content has-text-left" v-for="step in recipe.descriptions" :key="step.id">
                <div class="tags are-medium">
                    <span class="tag">{{step.descriptionnumber}}</span>
                </div>
                <hr>
                <div class="columns">
                    <div class="column">
                        <p class="description">{{step.description}}</p>
                    </div>
                    <div class="column">
                        <ul>
                            <li v-for="(ingredient,index) in step.ingredients" :key="index">{{ingredient.name}}</li>
                        </ul>
                        <ul>
                            <li v-for="(equipment,index) in step.equipment" :key="index">{{equipment.name}}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    import axios from 'axios'
    import { uri } from '../config.js'

    export default {
        data(){
            return{
                recipe: [],
                tags: [],
                persons: 0
            }
        },
        mounted() {

            this.getAllRecipe();

        },
        methods: {
            getAllRecipe()
            {
                axios
                    .get(`${uri}recipes/${this.$route.params.id}`)
                    .then(r => (this.recipe = r.data.data, this.persons = r.data.data.persons));
            },
        }
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