<template>
    <transition-group class="todos" name="todos" tag="ul">
        <div 
            v-for="todo in todoItems"
            v-bind:key="todo.id"
            class="todos__block"
        >
            <li
                v-bind:class="toggleClass(todo)"
                v-on:click="$emit('todo:select', todo)"
            >
                [{{ todo.id }}] {{ todo.title }}
            </li>
            <span 
                v-if="isCloseButton"
                class="todos__close-button"
                v-on:click="$emit('todo:remove', todo)"
            >x</span>
        </div>
    </transition-group>
</template>

<script>
export default {
    props: {
        todoItems: {
            type: Array,
            require: true
        },
        isCloseButton: {
            type: Boolean,
            require: false
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
.todos__block {
    display: flex;
    align-items: center;
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

.todos__close-button {
    background-color: #eee;
    padding: 2px 5px;
    border-radius: 5px;
    transition: all .1s;
    margin-left: 10px;
    cursor: pointer;
}

.todos__close-button:hover {
    background-color: rgb(255, 104, 104);
}
</style>