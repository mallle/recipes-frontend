<template>
    <div class="container">
        <div class="section">
            <h1 class="title is-1">
                Finde Rezept
            </h1>
        </div>
        <div class="section">
            <Tags :tags="tags"  @getRequestedResipes="getRequestedResipes"></Tags>
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
            getRequestedResipes(data){

                this.$router.push(`/tags/${data.tagId}?tag=${data.tagName}`)

            }
        }
    }
</script>

<style scoped>

</style>