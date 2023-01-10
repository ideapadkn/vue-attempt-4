<template>
  <div class="app">
    
    <form class="form">
      <h4 class="title">Create Post</h4>
      <input 
        v-model="this.title"
        class="input" 
        type="text" 
        placeholder="Name"
      >
      <input 
        v-model="this.body"
        class="input" 
        type="text" 
        placeholder="Description"
      >
      <button 
        class="btn"
        @click="createPost"
      >
        Create
      </button>
    </form>


    <div 
      class="post" 
      v-for="post in posts"
    >
      <div><strong>Name:</strong> {{ post.title }}</div>
      <div><strong>Description:</strong> {{ post.body }}</div>
    </div>

  </div>
</template>

<script>
  export default {
    data() {
      return {
        posts: [
          {id: 1, title: "JavaScript", body: "Description"},
          {id: 2, title: "JavaScript 2", body: "Description"},
          {id: 3, title: "JavaScript 3", body: "Description"},
          {id: 4, title: "JavaScript 4", body: "Description"},
        ],
        title: '',
        body: '',
      }
    },
    methods: {

    }, 
  }
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.post {
  border: 2px solid teal;
  padding: 15px;
  margin-top: 15px;
}
.app {
  padding: 20px;
}
.form {
  display: flex;
  flex-direction: column;
}
.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
.input:focus {
  outline: none;
}
.btn {
  align-self: flex-end;
  padding: 10px 15px;
  border: 1px solid teal;
  margin-top: 15px;
  background-color: transparent;
  transition: all .3s;
  cursor: pointer;
  color: teal;
}
.btn:hover {
  background-color: teal;
  color: #fff;
}
</style>

// single file component 