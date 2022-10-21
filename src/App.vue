<template>
    <!-- <nav>
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
    </nav> -->
    <menu_component />
    <router-view style="margin:100px 0" />
    <footer_component />
</template>
<script>
import menu_component from '@/components/menu.vue'
import footer_component from '@/components/footer.vue'
export default {
    name: 'HomeView',
    components: {
        menu_component,
        footer_component
    }
}
</script>
<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

nav {
    padding: 30px;
}

nav a {
    font-weight: bold;
    color: #2c3e50;
}

nav a.router-link-exact-active {
    color: #42b983;
}
</style>
