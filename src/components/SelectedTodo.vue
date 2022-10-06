<template>
    <ViewTodoItems
        v-bind:todo-items="selectedTodo"
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
    }
}
</script>

<style scoped>

</style>