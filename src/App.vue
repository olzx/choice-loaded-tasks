<template>
    <div id="app">
        <ViewTodo></ViewTodo>
    </div>
</template>

<script>
import ViewTodo from './components/ViewTodo.vue'

export default {
    name: 'App',
    components: {
        ViewTodo
    }
}
</script>

<style>
#app {
    font-family: Helvetica, Arial, sans-serif;
    color: #2c3e50;
}
</style>
