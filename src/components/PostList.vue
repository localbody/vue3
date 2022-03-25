<template>
    <div class="post" v-for="post in posts">
        <div>
            <strong>Название: </strong>
            <span>{{ post.title }}</span>
        </div>
        <div>
            <strong>Содержание: </strong>
            <span>{{ post.body }}</span>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        posts: {
            type: Array,
            required: true,
        },
    }

}
</script>

<style scoped>
    .post {
        padding: 15px;
        border: 1px solid forestgreen;
        margin-bottom: 5px;
    }
</style>
