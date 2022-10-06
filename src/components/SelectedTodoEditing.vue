<template>
    <input 
        class="editing__input" 
        type="text" 
        v-model="changedTitleTodo"
        v-bind:size="getInputLength(activeTodo.title?.length)"
        v-on:keyup.enter="submit"
        placeholder="Select todo"
    >
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
        }
    }
}
</script>

<style scoped>
.editing__input {
    text-align: center;
}
</style>