<template>
    <section>
        <ViewTodoItems v-bind:todo-items="todoItems"></ViewTodoItems>
        <ViewTodoPagination v-bind:amount-pages="amountPages"></ViewTodoPagination>
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

        }
    }
}
</script>