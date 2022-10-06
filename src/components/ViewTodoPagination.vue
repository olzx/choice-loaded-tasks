<template>
    <div class="pagination">
        <span
            v-for="page in amountPages"
            v-bind:key="page"
            v-on:click="onClickPage(page)"
            v-bind:class="toggleClass(page)"
        >
            {{ page }}
        </span>
    </div>
</template>

<script>
export default {
    props: {
        amountPages: {
            type: Number,
            require: true
        }
    },
    data: function() {
        return {
            activePage: 1
        }
    },
    methods: {
        onClickPage: function(page) {
            this.$emit('pagination:toggle', page)
            this.activePage = page
        },
        toggleClass: function(page) {
            return [
                { 
                    'pagination__active': page === this.activePage 
                }, 
                'pagination__page'
            ]
        }
    }
}
</script>

<style scoped>
.pagination {
    width: 100%;
    text-align: center;
}
.pagination__page {
    padding: 5px 20px;
    border: 1px solid rgb(0, 0, 0);
    background-color: #eee;
    cursor: pointer;
    transition: all .1s;
    border-radius: 4px;
}
.pagination__page:not(:first-child) {
    margin-left: 10px;
}
.pagination__page:hover {
    background-color: #bbb;
}
.pagination__active {
    background-color: #bbb;
}
</style>