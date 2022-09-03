<template>
  <h2 class="title">Adding new post</h2>
  <form class="formContainer" @submit.prevent>
    <my-input
        type="text"
        placeholder="title"
        v-model:value="post.title"
    />
    <my-input
        type="text"
        placeholder="body"
        v-model:value="post.body"
    />
    <my-button class="formBtn" @click="createPost">add post</my-button>
  </form>
</template>

<script>
export default {
  name: 'add-form',
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
      }
    },
  },
  props: {
  }
}
</script>

<style>
.title {
  align-self: flex-start;
}
.formContainer {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.formBtn {
  margin-top: 10px;
  align-self: end;
}

</style>