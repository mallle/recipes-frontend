<template>
    <nav class="navbar" role="navigation" aria-label="main navigation">
        <div class="navbar-brand">
            <a class="navbar-item" href="/">
                <img alt="Vue logo" src="../assets/logo.png">
            </a>

            <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample"
               :class="{'is-active': isActive}" @click="isActive = !isActive">
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
            </a>
        </div>

        <div id="navbarBasicExample" class="navbar-menu" :class="{'is-active': isActive}">
            <div class="navbar-start">

                <router-link to="/tags" tag="a" class="navbar-item" >Tags</router-link>

            </div>
        </div>
    </nav>
</template>

<script>
    export default {
        name: "Navbar.vue",
        data() {
            return { isActive: false }
        }

    }
</script>

<style scoped>

</style>