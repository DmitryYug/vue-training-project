<template>
  <div class="postListContainer" v-show="posts.length > 0" >
    <div v-for="post in posts" v-bind:key="post.id">
      <post-item
          @remove="$emit('remove', post)"
          :post="post"
          :key="post.id"
      />
    </div>
  </div>
  <h2 v-show="posts.length === 0" class="redText">! Empty List !</h2>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: 'posts-list',
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    }
  },
}
</script>

<style>
.title {
  align-self: flex-start;
}
.redText {
  color: red;
}
.postListContainer {
  width: 100%;
}
</style>