<template>
    <ViewTodoItems
        v-bind:todo-items="selectedTodo"
        v-on:todo:select="todoSelected"
    ></ViewTodoItems>
</template>

<script>
import ViewTodoItems from './ViewTodoItems.vue'

export default {
    props: {
        selectedTodo: {
            type: Array,
            require: true
        }
    },
    components: {
        ViewTodoItems
    },
    data: function() {
        return {
            
        }
    },
    methods: {
        todoSelected: function(todo) {
            console.log('Selected: ', todo)
        }
    }
}
</script>

<style scoped>

</style>