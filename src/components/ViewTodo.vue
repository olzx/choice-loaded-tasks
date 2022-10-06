<template>
    <ViewTodoControls
        v-bind:todo-items="todos" 
        v-bind:amount-pages="amountPages"
        v-on:todo:select="$emit('todo:select', $event)"
    ></ViewTodoControls>
</template>

<script>
import ViewTodoControls from './ViewTodoControls.vue'

export default {
    data: function() {
        return {
            todos: [
                {
                    id: 0,
                    completed: true,
                    title: 'New task',
                    userId: 0
                }
            ],
            amountPages: 5
        }
    },
    components: {
        ViewTodoControls
    },
    methods: {
        capitalizeFirstLetter: function(string) {
            return string.charAt(0).toUpperCase() + string.slice(1)
        },
        firstLetterArray(array) {
            for(let i = 0; i < array.length; i++) {
                array[i].title = this.capitalizeFirstLetter(array[i].title)
            }
            return array
        }
    },
    mounted: function() {
        this.axios.get('https://jsonplaceholder.typicode.com/todos')
            .then(response => response.data)
            .then(data => this.firstLetterArray(data))
            .then(modify => this.todos = modify)
            .catch(err => console.log('[Error]: ', err))
    }
}
</script>

<style>

</style>