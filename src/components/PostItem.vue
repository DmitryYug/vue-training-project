<template>
  <div class="postContainer">
    <div class="textBlock">
      <div><strong>{{ post.title }}</strong></div>
      <span>{{ post.body }}</span>
    </div>
    <my-button @click="$emit('remove', post)">remove post</my-button>
  </div>
</template>

<script>
export default {
  name: 'post-item',
  props: {
    post: {
      type: Object,
      required: true
    }
  },
}
</script>

<style>

.postContainer {
  padding: 10px;
  border: 1px solid black;
  margin: 10px 0 0 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.textBlock {
  padding: 0 20px 0 0;
}
</style>