<template>
    <div class="preloader__box">
        <div class="preloader__container">
            <span class="preloader__circle"></span>
            <span class="preloader__circle"></span>
            <span class="preloader__circle"></span>
            <span class="preloader__circle"></span>
        </div>
    </div>
</template>

<script>

</script>

<style scoped>
.preloader__box {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.preloader__container {
    height: 15px;
    width: 105px;
    display: flex;
    position: relative;
}

.preloader__container .preloader__circle {
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background-color: #bbb;
    animation: move 500ms linear 0ms infinite;
    margin-right: 30px;
}

.preloader__container .preloader__circle:first-child {
    position: absolute;
    top: 0;
    left: 0;
    animation: grow 500ms linear 0ms infinite;
}

.preloader__container .preloader__circle:last-child {
    position: absolute;
    top: 0;
    right: 0;
    margin-right: 0;
    animation: grow 500ms linear 0s infinite reverse;
}

@keyframes grow {
    from {
        transform: scale(0, 0);
        opacity: 0;
    }

    to {
        transform: scale(1, 1);
        opacity: 1;
    }
}

@keyframes move {
    from {
        transform: translateX(0px);
    }

    to {
        transform: translateX(45px);
    }
}
</style>