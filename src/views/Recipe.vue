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
        </div>
        <div class="section">
            <div class="columns is-centered">
                <div class="column">
                    <h3 class="title is-3">Zutaten</h3>
                    <table class="table is-narrow">
                        <tbody>
                            <tr v-for="(ingredient, index) in recipe.ingredients" :key="index">
                                <td class="has-text-right">{{ amount(ingredient.amount_per_person)}}<td>
                                <td>{{ingredient.type }} {{ingredient.name }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div class="column">
                    <h3 class="title is-3">Utensilien</h3>
                    <ul>
                        <li v-for="(equipment,index) in equipments" :key="index">{{equipment.name}}</li>
                    </ul>
                </div>
            </div>
        </div>
        <div class="section">
            <div class="columns has-text-left">
                <div class="column is-6">
                    <h4 class="title is-4"><span  class="description">To do</span></h4>
                </div>
                <div class="column">
                    <h4 class="title is-4">Zutaten</h4>

                </div>
                <div class="column">
                    <h4 class="title is-4">Utensilien</h4>
                </div>
            </div>
            <div class="content has-text-left" v-for="step in recipe.descriptions" :key="step.id">
                <div class="tags are-medium">
                    <span class="tag">{{step.descriptionnumber}}</span>
                </div>
                <hr>
                <div class="columns">
                    <div class="column is-6">
                        <p class="description">{{step.description}}</p>
                    </div>
                    <div class="column">
                        <ul>
                            <li v-for="(ingredient,index) in step.ingredients" :key="index">{{ingredient.name}}</li>
                        </ul>
                    </div>
                    <div class="column">

                        <ul>
                            <li v-for="(equipment,index) in step.equipment" :key="index">{{equipment.name}}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <div class="section">
            <h3 class="title is-3">Finde andere Rezepte mit gleichen Tags</h3>
                <Tags :tags="tags"  @getRequestedResipes="getRequestedResipes"></Tags>
        </div>
    </div>
</template>

<script>

    import axios from 'axios'
    import { uri } from '../config.js'

    import Tags from '@/components/Tags.vue'

    export default {
        data(){
            return{
                recipe: [],
                tags: [],
                persons: 0,
                equipments: null
            }
        },
        components: {
            Tags
        },
        mounted() {

            this.getAllRecipe();

        },
        methods: {
            getAllRecipe()
            {
                axios
                    .get(`${uri}recipes/${this.$route.params.id}`)
                    .then(r => (
                        this.recipe = r.data.data,
                        this.persons = r.data.data.persons,
                        this.equipments = r.data.data.equipment,
                        this.tags = r.data.data.tags
                    ));
            },
            amount(number){
                let amount = number * this.persons;
                return  amount.toFixed(2);
            },
            getRequestedResipes(data){
                console.log(data.tagId);
                this.$router.push(`/tags/${data.tagId}?tag=${data.tagName}`)

            }
        }
    }
</script>

<style scoped>
    .number-of-persons{
        margin: 0 3rem 0 3rem;
        font-size: 1.5rem;
    }
    .table td, .table th {
        border-color: white;
    }

    .table {
        margin-left: auto;
        margin-right: auto;
    }

    hr{
        margin: -2.5rem 8rem 1rem 51px;
    }

    .description{
        padding-left: 3.3rem;
    }
</style>