<template>
    <div class="header">
        <h1 class="header__text">Progress Meter Test</h1>
    </div>
</template>

<script>
export default {
    name: 'Header'
}
</script>

<style scoped>
.header {
    width: 100%;
    height: 100px;
    background-color: #00add0;
    
}
.header__text {
    display: flex;
    height: 100%;
    width: 100%;
    justify-content: center;
    align-items: center;
    color: #fff;
}
</style>
