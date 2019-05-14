<template>
    <div>
        <p>test</p>
    </div>
</template>

<script>
    export default {
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