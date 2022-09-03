<template>
  <div class="appContainer">
<!--header-->
    <h2 class="title">Post list</h2>
    <my-button @click="fetchPosts">fetch posts</my-button>
<!--    <input v-model="test"/>-->
    <my-button class="addBtn" @click="showModal">
      add post
    </my-button>
<!--add post modal-->
    <my-modal v-model:show="openModal">
      <add-form @create="createPost"/>
    </my-modal>
<!--post list-->
    <posts-list :posts="posts" @remove="removePost"/>

  </div>
</template>

<script>
import AddForm from "@/components/AddForm";
import PostsList from "@/components/PostsList";
import MyModal from "@/components/UI/MyModal";
import MyButton from "@/components/UI/MyButton";
import axios from "axios";

export default {
  name: 'app',
  components: {MyButton, MyModal, PostsList, AddForm},
  data() {
    return {
      posts: [
        {id: 1, title: 'Post 1', body: 'here will be post 1 text'},
        {id: 2, title: 'Post 2', body: 'here will be post 2 text'},
        {id: 3, title: 'Post 3', body: 'here will be post 3 text'}
      ],
      openModal: false,
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.openModal = false
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showModal() {
      this.openModal = true
    },
    hideModal(status) {
      this.openModal = status
    },
    async fetchPosts() {
      try {
        let response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = response.data
        console.log(response)
      }
      catch (e) {
        console.log('error')
      }
    }
  }
}
</script>

<style>
.appContainer {
  margin: 0 auto;
  width: 500px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

.addBtn {
  align-self: flex-start;
}
</style>

