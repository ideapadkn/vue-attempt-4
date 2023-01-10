<template>
  <div 
      class="post" 
      v-for="post in posts"
  >
    <div><strong>Name:</strong> {{ post.title }}</div>
    <div><strong>Description:</strong> {{ post.body }}</div>
  </div>
</template>

<script>
  export default {
    props: {
      posts: {
        type: Array,
        requiered: true,
      },
    }
  }
</script>

<style scoped>
.post {
  border: 2px solid teal;
  padding: 15px;
  margin-top: 15px;
}
</style>