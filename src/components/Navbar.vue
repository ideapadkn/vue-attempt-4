<template>
  <div class="navbar">
    <div 
      @click="$router.push('/')"
      class="title"
    >
      Vue 3
    </div>
    <div class="navbar__btns">
      <my-button @click="$router.push('/users')">Users</my-button>
      <my-button @click="$router.push('/about')" style="margin-left: 20px;">About</my-button>
    </div>
  </div>
</template>

<script>
  export default {
    
  }
</script>

<style scoped>
.title {
  font-size: 24px;
  font-weight: 700;
  cursor: pointer;
}
.navbar {
  height: 50px;
  background-color: rgb(216, 220, 220);
  box-shadow: 2px 2px 4px gray;
  display: flex;
  align-items: center;
  padding: 0 15px;
}
.navbar__btns {
  margin-left: auto;
}
</style>