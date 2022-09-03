<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button',
}
</script>

<style>
.button {
  /*width: 100px;*/
  /*height: 30px;*/
}
</style>