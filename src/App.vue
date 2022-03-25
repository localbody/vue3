<template>
    <div class="app">
        <post-form
            @create="createPost"
        />
        <post-list
            :posts="posts"
        />
    </div>

</template>

<script>

    import PostForm from '@/components/PostForm.vue'
    import PostList from '@/components/PostList.vue'

    export default {
        components: {
            PostForm,
            PostList,
        },
        data() {
            return {
                posts: [
                    {id: 1, title: 'JS', body: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat veritatis facere maiores minima doloribus reiciendis qui eum consequatur consectetur. Ullam, quod. At nam modi amet dolorem a inventore neque excepturi!'},
                    {id: 2, title: 'Python', body: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat veritatis a inventore neque excepturi!'},
                    {id: 3, title: 'CSS', body: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat veritatis facere!'},
                ],
            }
        },
        methods: {
            createPost(post) {
                this.posts.push(post);
            }
        }
    }

</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .app {
        padding: 20px;
    }
</style>
