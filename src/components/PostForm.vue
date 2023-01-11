<template>
  <form class="form" @submit.prevent>
    <h4 class="title">Create Post</h4>
    <my-input 
      v-model="post.title"
      class="input" 
      type="text" 
      placeholder="Name"
    />
    <my-input 
      v-model="post.body"
      class="input" 
      type="text" 
      placeholder="Description"
    />
    <my-button
      class="btn"
      style="margin-top: 15px;"
      @click="createPost"
    >
      Create
    </my-button>
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
</style>