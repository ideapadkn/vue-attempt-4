<template>
  <div class="app">
    <h1>Posts</h1>
    <my-button
      @click="showDialog"
      style="margin: 15px 0;"
    >
      Create
    </my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form 
      @create="createPost"
    />
    </my-dialog>
    
    <post-list
      :posts="posts" 
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div v-else>
      loading..
    </div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm"
import PostList from "@/components/PostList"
import axios from 'axios'
  export default {
    components: {
      PostForm,
      PostList
    },  
    data() {
      return {
        posts: [],
        dialogVisible: false,
        isPostsLoading: false,
      }
    },
    methods: {
      createPost(post) {
        this.posts.push(post);
        this.dialogVisible = false;
      },
      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id)
      },
      showDialog() {
        this.dialogVisible = true;
      },
      async fetchPosts() {
        try {
          this.isPostsLoading = true;
          setTimeout( async () => {
            const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?_limit=10`);
            this.posts = response.data;
            this.isPostsLoading = false;
          }, 1000)
        } catch (e) {
          alert('error')
        } finally {
          
        }
      },
    },
    mounted() {
      this.fetchPosts();
    },   
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

// single file component 