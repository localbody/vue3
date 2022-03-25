<template>
    <form @submit.prevent>
        <input
            v-model="post.title"
            type="text"
            placeholder="Название"
        >
        <input
            v-model="post.body"
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
    data() {
        return {
            post: {
                title: '',
                body: '',
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: '',
            }
        }
    }

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
