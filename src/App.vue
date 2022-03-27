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
        <div class="pages">
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
        </div>
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
            changePage(pageNumber) {
                this.page = pageNumber;
            },
            async fetchPosts() {
                try {
                    this.isPostLoading = true;
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                        params: {
                            _page: this.page,
                            _limit: this.limit,
                        }
                    });
                    this.totalPages = Math.ceil( response.headers['x-total-count'] / this.limit );
                    this.posts = response.data;
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
            page() {
                this.fetchPosts();
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
