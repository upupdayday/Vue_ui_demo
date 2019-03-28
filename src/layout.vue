<template>
    <div class="layout">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: "gLayout"
    }
</script>

<style lang="scss" scoped>
    .layout{
        display: flex;
        flex-direction: column;
    }

</style>