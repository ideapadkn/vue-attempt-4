<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
  export default {
    name: 'my-button'
  }
</script>

<style scoped>
.btn {
  align-self: flex-end;
  padding: 10px 15px;
  border: 1px solid teal;
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