<template>
  <div class="app">
    <h1>Posts</h1>
    <my-input 
      v-model="searchQuery"
      placeholder="Search"
    />
    <div class="app__btns">
      <my-button
        @click="showDialog"
      >
        Create
      </my-button>
      <my-select 
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>
    
    <my-dialog v-model:show="dialogVisible">
      <post-form 
      @create="createPost"
    />
    </my-dialog>
    
    <post-list
      :posts="sortedAndSearchedPosts" 
      @remove="removePost"
    />
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
        selectedSort: '',
        searchQuery: '',
        sortOptions: [
          {value: 'title', name: 'name'},
          {value: 'body', name: 'description'},
        ]
      }
    },
    methods: {
      createPost(post) {
        this.posts.push(post);
        this.dialogVisible = false;
      },
      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id);
      },
      showDialog() {
        this.dialogVisible = true;
      },
      async fetchPosts() {
        try {
          const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?_limit=10`);
          this.posts = response.data;
          
        } catch (e) {
          alert('error');
        } finally {
          this.isPostsLoading = false;
        }
      },
    },
    mounted() {
      this.fetchPosts();
    },   
    computed: {
      sortedPosts() {
        return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },  
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    },
            // watch: {
            //   // selectedSort(newValue) {
            //   //   this.posts.sort((post1, post2) => {
            //   //     return post1[newValue]?.localeCompare(post2[newValue]);
            //   //   })
            //   },
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
.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
</style>

// single file component 