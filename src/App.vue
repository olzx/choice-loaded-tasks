<template>
    <div id="app">
        <ViewTodos></ViewTodos>
    </div>
</template>

<script>
import ViewTodos from './components/view-todos'

export default {
    name: 'App',
    components: {
        ViewTodos
    }
}
</script>

<style>
#app {
    font-family: Helvetica, Arial, sans-serif;
    color: #2c3e50;
}
</style>
