<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: 'my-button'
}
</script>

<style scoped>
    .btn {
        padding: 0 1em;
        height: 2em;
        background-color: transparent;
        border: 1px solid forestgreen;
        color: forestgreen;
    }

</style>
