<template>
    <div class="app">
        <my-dialog
            v-model:show="dialogVisible"
        >
            <post-form
                @create="createPost"
            />
        </my-dialog>

        <h1>Страница с постами</h1>

        <div class="app__btns">
            <my-input
                v-model="searchQuery"
            />
            <my-select
                v-model="selectedSort"
                :options="sortedOptions"
            />
            <my-button
                @click="showDialog"
            >
                Создать пост
            </my-button>
        </div>

        <post-list
            v-if="!isPostLoading"
            :posts="sortedAndSearchedPosts"
            @remove="removePost"
        />
        <div v-else>Идет загрузка...</div>
        <!-- <div class="pages">
            <div
                v-for="pageNumber in totalPages"
                :key="pageNumber"
                class="page"
                :class="{
                    'page--current' : pageNumber === page
                }"
                @click="changePage(pageNumber)"
            >
                {{pageNumber}}
            </div>
        </div> -->
    </div>

</template>

<script>

    import PostForm from '@/components/PostForm.vue';
    import PostList from '@/components/PostList.vue';
    import axios from 'axios';

    export default {
        components: {
            PostForm,
            PostList,
        },
        data() {
            return {
                posts: [],
                dialogVisible: false,
                isPostLoading: false,
                selectedSort: '',
                sortedOptions: [
                    {value: 'title', name: 'По названию'},
                    {value: 'body', name: 'По описанию'},
                ],
                searchQuery: '',
                page: 1,
                limit: 10,
                totalPages: 0,
            }
        },
        methods: {
            createPost(post) {
                this.posts.push(post);
                this.dialogVisible = false;
            },
            removePost(post) {
                this.posts = this.posts.filter( p => p.id !== post.id);
            },
            showDialog() {
                this.dialogVisible = true;
            },
            // changePage(pageNumber) {
            //     this.page = pageNumber;
            // },
            async fetchPosts() {
                try {
                    this.isPostLoading = true;

                    // const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    //     params: {
                    //         _page: this.page,
                    //         _limit: this.limit,
                    //     }
                    // });
                    // this.totalPages = Math.ceil( response.headers['x-total-count'] / this.limit );
                    // this.posts = response.data;

                    const response = await axios.get('http://energy13:8080/rest/users/1', {
                        params: {
                        }
                    });
                    console.log(response.data);

                    this.posts = [
                                    {
                                        "userId": 1,
                                        "id": 1,
                                        "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
                                        "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
                                    },
                                    {
                                        "userId": 1,
                                        "id": 2,
                                        "title": "qui est esse",
                                        "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
                                    },
                                    {
                                        "userId": 1,
                                        "id": 3,
                                        "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
                                        "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
                                    },
                                    {
                                        "userId": 1,
                                        "id": 4,
                                        "title": "eum et est occaecati",
                                        "body": "ullam et saepe reiciendis voluptatem adipisci\nsit amet autem assumenda provident rerum culpa\nquis hic commodi nesciunt rem tenetur doloremque ipsam iure\nquis sunt voluptatem rerum illo velit"
                                    },
                                    {
                                        "userId": 1,
                                        "id": 5,
                                        "title": "nesciunt quas odio",
                                        "body": "repudiandae veniam quaerat sunt sed\nalias aut fugiat sit autem sed est\nvoluptatem omnis possimus esse voluptatibus quis\nest aut tenetur dolor neque"
                                    },
                                    {
                                        "userId": 1,
                                        "id": 6,
                                        "title": "dolorem eum magni eos aperiam quia",
                                        "body": "ut aspernatur corporis harum nihil quis provident sequi\nmollitia nobis aliquid molestiae\nperspiciatis et ea nemo ab reprehenderit accusantium quas\nvoluptate dolores velit et doloremque molestiae"
                                    },
                                    {
                                        "userId": 1,
                                        "id": 7,
                                        "title": "magnam facilis autem",
                                        "body": "dolore placeat quibusdam ea quo vitae\nmagni quis enim qui quis quo nemo aut saepe\nquidem repellat excepturi ut quia\nsunt ut sequi eos ea sed quas"
                                    },
                                ];

                }
                catch (e) {
                    alert(e);
                }
                finally {
                    this.isPostLoading = false;
                }
            },
        },
        mounted() {
            this.fetchPosts();
        },
        computed: {
            sortedPosts() {
                return [...this.posts].sort((post1, post2) => {
                    return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]);
                })
            },
            sortedAndSearchedPosts() {
                return this.sortedPosts.filter( post => post.title.includes(this.searchQuery) );
            }
        },
        watch: {
            // page() {
            //     this.fetchPosts();
            // }
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

    .app__btns {
        display: grid;
        gap: 1em;
    }

    .pages {
        display: flex;
        justify-content: space-between;
    }

    .page {
        padding: 0.5em 0;
        border: 1px solid forestgreen;
        min-width: 2em;
        text-align: center;
    }

    .page--current {
        background-color: greenyellow;
    }
</style>
