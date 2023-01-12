<template>
  <div 
    v-if="posts.length > 0"
  >
    <h3>List Users</h3>
    <transition-group name="post-list">
      <post-item 
        v-for="post in posts" 
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
      />
    </transition-group>
  </div>
  <h2
    v-else
    style="color: red;"
  >
    Post List Empty
  </h2>
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
.post-list-move,
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.5s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>