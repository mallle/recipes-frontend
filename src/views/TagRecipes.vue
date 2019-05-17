<template>
    <div class="container">
        <div class="section">
            <Tags :tags="tags"  @getRequestedResipes="getRequestedResipes"></Tags>
        </div>
        <div class="section">
            <h1 class="title is-1">Rezepte für den Tag "{{ tag }}"</h1>
        </div>

        <div class="section">
            <div class="columns is-multiline">
                <div class="column is-4" v-for="(recipe,index) in recipes" :key="index" >
                    <RecipeCard  :id="recipe.id" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Tags from '@/components/Tags.vue'
    import RecipeCard from '@/components/RecipeCard.vue'

    import axios from 'axios'
    import { uri } from '../config'

    export default {
        name: "Tags.vue",
        data() {
            return {
                tag: '',
                tags: null,
                recipes: null
            }
        },
        components: {
            Tags,
            RecipeCard
        },
        mounted() {

            this.getAllTags()

            let data = {
                tagId: this.$route.params.id,
                tagName: this.$route.query.tag
            };

            if(data){

                this.requestedResipes(data);

            }
        },
        methods: {
            getAllTags()
            {
                axios.get(uri + 'tags')
                    .then(response => {
                        this.tags = response.data.data;
                    })
                    .catch(error => {
                        console.log(error.response)
                    });
            },
            requestedResipes(data) {
                this.tag = data.tagName
                axios.get(uri + 'tags/' +  data.tagId + '/recipes')
                    .then(response => {
                        this.recipes = response.data.data;
                    })
                    .catch(error => {
                        console.log(error.response)
                    });
            },
            getRequestedResipes(data){
                this.requestedResipes(data)
                this.$router.push(`/tags/${data.tagId}`)
            }
        }
    }
</script>

<style scoped>

</style>