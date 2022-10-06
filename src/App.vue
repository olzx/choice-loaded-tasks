<template>
    <div id="app" class="todo-blocks">
        <SelectedTodo v-bind:selected-todo="todoSelectedDataBase" v-on:todo:remove="todoRemoved"></SelectedTodo>
        <ViewTodo v-on:todo:select="todoSelected"></ViewTodo>
    </div>
</template>

<script>
import ViewTodo from './components/ViewTodo.vue'
import SelectedTodo from './components/SelectedTodo.vue'

export default {
    name: 'App',
    components: {
        ViewTodo,
        SelectedTodo
    },
    data: function() {
        return {
            todoSelectedDataBase: []
        }
    },
    methods: {
        todoSelected: function(todo) {
            const isFound = this.todoSelectedDataBase.indexOf(todo)
            if (isFound === -1) {
                this.todoSelectedDataBase.push(todo)
            }
        },
        todoRemoved: function(todo) {
            const isFound = this.todoSelectedDataBase.indexOf(todo)
            if (isFound !== -1) {
                this.todoSelectedDataBase.splice(isFound, 1)
            }
        }
    }
}
</script>

<style>
#app {
    font-family: Helvetica, Arial, sans-serif;
    color: #2c3e50;
}
.todo-blocks {
    display: flex;
    max-width: 1210px;
    justify-content: space-between;
    margin: 0 auto;
}

@media (max-width: 1222px) {
    .todo-blocks {
        flex-direction: column;
    }
}
</style>
