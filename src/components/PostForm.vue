<template>
    <form @submit.prevent>
        <input
            v-bind:value="title"
            @input="title = $event.target.value"
            type="text"
            placeholder="Название"
        >
        <input
            v-bind:value="body"
            @input="body = $event.target.value"
            type="text"
            placeholder="Описание"
        >
        <button
            @click="createPost"
            class="btn"
        >Создать</button>
    </form>
</template>

<script>
export default {

}
</script>

<style scoped>
    form {
        display: grid;
        grid-template-rows: repeat(3, 2em);
        gap: 1em;
        margin-bottom: 2em;
    }

    .btn {
        justify-self: start;
        padding: 0 2em;
    }

    input {
        padding: 0 1em;
    }
</style>
