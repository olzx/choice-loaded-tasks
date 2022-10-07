<template>
    <div id="app" v-bind:class="{'todo-blocks': !viewPreload}">
        <PreloaderItem v-if="viewPreload"></PreloaderItem>
        <SelectedTodo 
            v-bind:selected-todo="todoSelectedDataBase" 
            v-on:todo:remove="todoRemoved"
            v-on:editing-todo="changedTodo"
            v-on:completed-toggle="completedToggle"
            v-bind:class="[{'todo-blocks__block_disabled': viewPreload}, 'todo-blocks__block']"
        ></SelectedTodo>
        <ViewTodo 
            v-on:todo:select="todoSelected"
            v-on:todo-loaded="todoLoaded"
            v-bind:class="[{'todo-blocks__block_disabled': viewPreload}, 'todo-blocks__block']"
        ></ViewTodo>
    </div>
</template>

<script>
import ViewTodo from './components/ViewTodo.vue'
import SelectedTodo from './components/SelectedTodo.vue'
import PreloaderItem from './components/PreloaderItem.vue'

export default {
    name: 'App',
    components: {
        ViewTodo,
        SelectedTodo,
        PreloaderItem
    },
    data: function() {
        return {
            todoSelectedDataBase: [],
            viewPreload: true
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
        },
        changedTodo: function(objectChange) {
            const isFound = this.todoSelectedDataBase.indexOf(objectChange.todo)
            if (isFound !== -1) {
                this.todoSelectedDataBase[isFound].title = objectChange.newTitle
            }
        },
        completedToggle: function(todo) {
            const isFound = this.todoSelectedDataBase.indexOf(todo)
            if (isFound !== -1) {
                const completed = this.todoSelectedDataBase[isFound].completed
                this.todoSelectedDataBase[isFound].completed = !completed
            }
        },
        viewPreloaderToggle() {
            const vm = this
            setTimeout(function() {vm.viewPreload = !vm.viewPreload}, 1000)
        },
        todoLoaded: function() {
            this.viewPreloaderToggle()
        }
    }
}
</script>

<style>
body {
    margin: 0;
}
#app {
    font-family: Helvetica, Arial, sans-serif;
    color: #2c3e50;
}
.todo-blocks {
    display: flex;
    max-width: 1220px;
    justify-content: space-between;
    margin: 0 auto;
}
.todo-blocks__block {
    max-width: 615px;
}

@media (max-width: 1222px) {
    .todo-blocks {
        flex-direction: column;
    }
    .todo-blocks__block {
        margin: 0 auto;
    }
}

.todo-blocks__block_disabled {
    display: none;
}
</style>
