<template>
    <transition-group class="todos" name="todos" tag="ul" mode="out-in">
        <li 
            v-for="todo in todoItems"
            v-bind:key="todo.id"
            v-bind:class="toggleClass(todo)"
            v-on:click="$emit('todo:select', todo)"
        >
            [{{ todo.id }}] {{ todo.title }}
        </li>
    </transition-group>
</template>

<script>
export default {
    props: {
        todoItems: {
            type: Array,
            require: true
        }
    },
    methods: {
        toggleClass: function(todo) {
            const isCompleted = todo.completed
            let classList = 'todo '
            classList += isCompleted ? 'todo_completed_true' : 'todo_completed_false'
            return classList
        }
    }
}
</script>

<style scoped>
.todos {
    list-style: none;
}
.todo {
    position: relative;
    cursor: pointer;
}
.todo_completed_true::before {
    content: '';
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: rgb(0, 128, 64);
    border-radius: 50%;
    left: -14px;
    top: 4px;
}
.todo_completed_false::before {
    content: '';
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: rgb(201, 0, 0);
    border-radius: 50%;
    left: -14px;
    top: 4px;
}

.todos-leave-active {
    display: none;
}
.todos-enter {
    opacity: 0;
}
.todos-enter-active {
    transition: opacity .2s ease-in-out;
}
</style>