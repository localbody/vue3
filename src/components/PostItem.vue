<template>
    <div class="post">
        <div>
            <h4>{{post.id}}</h4>
            <div>
                <strong>Название: </strong>
                <span>{{ post.title }}</span>
            </div>
            <div>
                <strong>Содержание: </strong>
                <span>{{ post.body }}</span>
            </div>
        </div>
        <div class="post__btns">
            <my-button
                @click="$emit('remove', post)"
            >Удалить</my-button>
        </div>
    </div>
</template>

<script>

export default {
    props: {
        post: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style scoped>
    .post {
        padding: 15px;
        border: 1px solid forestgreen;
        margin-bottom: 5px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>
