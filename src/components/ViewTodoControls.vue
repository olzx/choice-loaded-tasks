<template>
    <section>
        <ViewTodoItems v-bind:todo-items="todoItems"></ViewTodoItems>
        <ViewTodoPagination v-bind:amount-pages="amountPages" v-on:pagination:toggle="togglePage"></ViewTodoPagination>
    </section>    
</template>

<script>
import ViewTodoItems from './ViewTodoItems.vue'
import ViewTodoPagination from './ViewTodoPagination.vue'

export default {
    props: {
        todoItems: {
            type: Array,
            require: true
        },
        amountPages: {
            type: Number,
            require: true
        }
    },
    components: {
        ViewTodoItems,
        ViewTodoPagination
    },
    data: function() {
        return {
            itemsOnPage: this.countItemsOnPage()
        }
    },
    methods: {
        countItemsOnPage: function() {
            return this.todoItems.length / this.amountPages
        },
        togglePage: function(page) {
            console.log(page)
        }
    }
}
</script>