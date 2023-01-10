<template>
  <div>
    <h3>List Users</h3>
    <post-item 
      v-for="post in posts" 
      :post="post"
    />
  </div>
</template>

<script>
import PostItem from '@/components/PostItem';
  export default {
    components: {
      PostItem
    },
    props: {
      posts: {
        type: Array,
        requiered: true,
      },
    }
  }
</script>

<style scoped>

</style>