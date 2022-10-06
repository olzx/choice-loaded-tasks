<template>
    <div class="pagination">
        <span
            class="pagination__page"
            v-for="page in amountPages"
            v-bind:key="page"
            v-on:click="$emit('pagination:toggle', page)"
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
</style>