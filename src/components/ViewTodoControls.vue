<template>
    <section>
        <ViewTodoItems v-bind:todo-items="activeTodoItems" v-on:todo:select="$emit('todo:select', $event)"></ViewTodoItems>
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
            itemsOnPage: this.countItemsOnPage(),
            activeTodoItems: []
        }
    },
    methods: {
        countItemsOnPage: function() {
            return this.todoItems.length / this.amountPages
        },
        getOffsetItems: function(page) {
            const items = this.todoItems
            if (page === 1) {
                return items.slice(0, this.itemsOnPage)
            } else {
                const pageOffsetBefore = (page-1)*this.itemsOnPage
                const pageOffsetAfter = pageOffsetBefore + this.itemsOnPage

                return items.slice(pageOffsetBefore, pageOffsetAfter)
            }
        },
        togglePage: function(page) {
            this.activeTodoItems = this.getOffsetItems(page)
        }
    },
    beforeMount: function() {
        this.activeTodoItems = this.getOffsetItems(1)
        console.log('beforeMount')
    }
}
</script>