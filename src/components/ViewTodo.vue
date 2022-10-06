<template>
    <section>
        <ViewTodoItems v-bind:todo-items="todos"></ViewTodoItems>
        <ViewTodoPagination v-bind:amount-pages="amountPages"></ViewTodoPagination>
    </section>
</template>

<script>
import ViewTodoItems from './ViewTodoItems.vue'
import ViewTodoPagination from './ViewTodoPagination.vue'

export default {
    data: function() {
        return {
            todos: [],
            amountPages: 5
        }
    },
    components: {
        ViewTodoItems,
        ViewTodoPagination
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