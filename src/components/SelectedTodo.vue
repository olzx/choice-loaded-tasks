<template>
    <section>
        <SelectedTodoEditing 
            v-bind:active-todo="todoChange" 
            v-on:editing-todo="$emit('editing-todo', $event)"
        ></SelectedTodoEditing>
        <ViewTodoItems
            v-bind:todo-items="selectedTodo"
            v-bind:is-close-button="true"
            v-on:todo:select="todoSelected"
            v-on:todo:remove="$emit('todo:remove', $event)"
        ></ViewTodoItems>
    </section>
</template>

<script>
import ViewTodoItems from './ViewTodoItems.vue'
import SelectedTodoEditing from './SelectedTodoEditing.vue'

export default {
    props: {
        selectedTodo: {
            type: Array,
            require: true
        }
    },
    components: {
        ViewTodoItems,
        SelectedTodoEditing
    },
    data: function() {
        return {
            todoChange: {}
        }
    },
    methods: {
        todoSelected: function(todo) {
            this.todoChange = todo
            console.log('Selected: ', todo.title)
        }
    }
}
</script>

<style scoped>

</style>