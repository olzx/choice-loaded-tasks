<template>
        <ViewTodoItems v-bind:todo-items="todos"></ViewTodoItems>
</template>

<script>
import ViewTodoItems from './ViewTodoItems.vue'

export default {
    data: function() {
        return {
            todos: []
        }
    },
    components: {
        ViewTodoItems
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
    }
}
</script>

<style>

</style>