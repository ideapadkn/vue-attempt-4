<template>
  <div class="app">
    <post-form />
    <post-list
      :posts="posts"    
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm"
import PostList from "@/components/PostList"
  export default {
    components: {
      PostForm,
      PostList
    },  
    data() {
      return {
        posts: [
          {id: 1, title: "JavaScript", body: "Description"},
          {id: 2, title: "JavaScript 2", body: "Description"},
          {id: 3, title: "JavaScript 3", body: "Description"},
          {id: 4, title: "JavaScript 4", body: "Description"},
        ],
      }
    },
    methods: {
      createPost() {
        
      },
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