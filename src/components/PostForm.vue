<template>
  <form class="form" @submit.prevent>
    <h4 class="title">Create Post</h4>
    <input 
      v-model="post.title"
      class="input" 
      type="text" 
      placeholder="Name"
    >
    <input 
      v-model="post.body"
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
</template>

<script>
  export default {
    data() {
      return {
        post: {
          title: '',
          body: '',
        }
      }
    },
    methods: {
      createPost() {
        this.post.id = Date.now();
        this.$emit('create', this.post)
        this.post = {
          title: '',
          body: '',
        }
      }
    }
  }
</script>

<style scoped>
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