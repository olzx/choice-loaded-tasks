<template>
    <section>
        <h3 class="selected__title">Selected: {{ selectedTodo.length }}</h3>
        <SelectedTodoEditing 
            v-bind:active-todo="todoChange" 
            v-on:editing-todo="$emit('editing-todo', $event)"
            v-on:completed-toggle="$emit('completed-toggle', $event)"
        ></SelectedTodoEditing>
        <ViewTodoItems
            v-bind:todo-items="selectedTodo"
            v-bind:is-close-button="true"
            v-on:todo:select="todoSelected"
            v-on:todo:remove="onTodoRemove"
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
        },
        onTodoRemove: function($event) {
            this.$emit('todo:remove', $event)

            if ($event === this.todoChange) {
                this.todoChange = {}
            }
        }
    }
}
</script>

<style scoped>
.selected__title {
    margin-top: 0px;
    margin-bottom: 5px;
}
</style>