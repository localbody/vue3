<template>
    <h3>Новый пост</h3>
    <form @submit.prevent>
        <my-input
            v-model="post.title"
            placeholder="Название"
        />
        <my-input
            v-model="post.body"
            placeholder="Описание"
        />
        <my-button
            @click="createPost"
        >Создать</my-button>
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
    },

}
</script>

<style scoped>

    form {
        margin-top: 2em;
        display: grid;
        grid-template-rows: repeat(3, 2em);
        gap: 1em;
    }

</style>
