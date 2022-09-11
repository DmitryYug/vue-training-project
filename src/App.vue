<template>
  <div class="appContainer">

    <!--header-->
    <h2 class="title">Post list</h2>

    <my-input type="text" v-model:value="searchQuery" placeholder="search"/>

    <div class="buttonGroup">
      <my-button class="addBtn" @click="showModal">
        add post
      </my-button>
      <my-select
          :options="sortOptions"
          v-model:chosenOption="selectedSortOption"
      />
    </div>

    <!--add post modal-->
    <my-modal v-model:show="openModal">
      <add-form @create="createPost"/>
    </my-modal>

    <!--post list-->
    <posts-list
        :posts="sortedAndSearchedPosts"
        @remove="removePost"
        v-if="!isPostsLoading"
    />
    <pre-loader v-else/>
  </div>
</template>

<script>
import AddForm from "@/components/AddForm";
import PostsList from "@/components/PostsList";
import axios from "axios";

export default {

  name: 'app',
  components: {PostsList, AddForm},

  data() {
    return {
      posts: [],
      openModal: false,
      isPostsLoading: false,
      sortOptions: [
        {value: 'title', title: 'Sort by name'},
        {value: 'body', title: 'Sort by body'}
      ],
      selectedSortOption: '',
      searchQuery: ''
    }
  },

  mounted() {
    this.fetchPosts()
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
        this.isPostsLoading = true
        let response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = response.data
      } catch (e) {
        console.log('error')
      } finally {
        this.isPostsLoading = false
      }
    },
  },

  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSortOption]?.localeCompare(post2[this.selectedSortOption])
      })
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes((this.searchQuery).toLowerCase()))
    }
  },
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

.buttonGroup {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
</style>

