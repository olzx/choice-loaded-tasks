<template>
    <section class="editing">
        <input 
            class="editing__input" 
            type="text" 
            v-model="changedTitleTodo"
            v-bind:size="getInputLength(activeTodo.title?.length)"
            v-on:keyup.enter="submit"
            placeholder="Select todo"
        >
        <span 
            v-if="activeSelectedTodoIsEmpty()"
            class="editing__prompt"
        >
            Tub ENTER to save
        </span>
    </section>
</template>

<script>
export default {
    props: {
        activeTodo: {
            type: Object,
            require: true
        }
    },
    data: function() {
        return {
            changedTitleTodo: '',
            activeSelectedTodo: {}
        }
    },
    watch: {
        activeTodo: function(newTodo) {
            this.changedTitleTodo = newTodo.title
            this.activeSelectedTodo = newTodo
        }
    },
    methods: {
        getInputLength: function(length) {
            return length > 80 ? 80 : length
        },
        submit: function() {
            this.$emit('editing-todo', {
                todo: this.activeSelectedTodo,
                newTitle: this.changedTitleTodo
            })
        },
        activeSelectedTodoIsEmpty: function() {
            return Object.keys(this.activeSelectedTodo).length !== 0
        }
    }
}
</script>

<style scoped>
.editing {
    position: relative;
}
.editing__input {
    text-align: center;
}
.editing__prompt {
    position: absolute;
    left: 5px;
    bottom: -16px;
    font-size: 12px;
}
</style>