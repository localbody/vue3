<template>
    <div class="post">
        <div>
            <strong>Название:</strong>
            <span>Пост о JS</span>
        </div>
        <div>
            <strong>Описание:</strong>
            <span>Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat veritatis facere maiores minima doloribus reiciendis qui eum consequatur consectetur. Ullam, quod. At nam modi amet dolorem a inventore neque excepturi!</span>
        </div>


    </div>
</template>

<script>
    export default {
        data() {
            return {
                posts: [
                    {id: 1, title: 'JS', body: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat veritatis facere maiores minima doloribus reiciendis qui eum consequatur consectetur. Ullam, quod. At nam modi amet dolorem a inventore neque excepturi!'},
                    {id: 2, title: 'Python', body: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat veritatis a inventore neque excepturi!'},
                    {id: 3, title: 'CSS', body: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat veritatis facere!'},
                ]
            }
        },
        methods: {
            addLike() {
                this.likes += 1;
            },
            addDislike() {
                this.dislikes += 1;
            },
        }
    }

</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .post {
        padding: 15px;
        border: 1px solid forestgreen;
        margin: 5px;
    }
</style>
