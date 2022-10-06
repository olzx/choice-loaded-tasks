<template>
    <ViewTodoItems
        v-bind:todo-items="selectedTodo"
        v-bind:is-close-button="true"
        v-on:todo:select="todoSelected"
        v-on:todo:remove="$emit('todo:remove', $event)"
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