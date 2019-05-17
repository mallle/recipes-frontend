<template>
    <div class="section">
        <div class="buttons are-medium">
<!--            <a  class="button" type="is-info" size="is-medium" @click="getAllRecipes">All</a>-->
            <a  class="button" v-for="(tag, index) in tags" :key="index" type="is-info" size="is-medium" @click="getRecipes(tag.id, tag.name)">{{ tag.name }}</a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Tags.vue",
        props: {
            tags: Array
        },
        mounted() {
          console.log(this.tags);
        },
        methods: {
            getRecipes(tagId, tagName){
                var data = {
                    tagId: tagId,
                    tagName: tagName
                }
                this.$emit('getRequestedResipes', data);
            }
        }
    }
</script>

<style scoped>

</style>