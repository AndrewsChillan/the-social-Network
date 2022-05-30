<template>
  <h1>Home</h1>

  <Post
    v-for="post in posts"
    :key="post._id"
    :title="post.title"
    :content="post.content"
    :firstname="post.firstname"
    :lastname="post.lastname"
    :date="post.date"
  ></Post>

  <Pagination :totalPages="totalPages" @page-change="updatePage"></Pagination>
  <p v-if="error">
    Une erreur s'est produite lors de la récupération des posts
  </p>
</template>

<script>
import Post from "@/components/Post.vue";
import Pagination from "@/components/Pagination.vue";

export default {
  components: {
    Post,
    Pagination,
  },
  data() {
    return {
      posts: [],
      page: 0,
      totalPages: 0,
      error: false,
    };
  },
  mounted() {
    this.getPosts();
  },
  watch: {
    page() {
      this.getPosts();
    },
  },
  methods: {
    async getPosts() {
      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/demo/posts?page=" +
          this.page
      );
      const data = await response.json();
      console.log(data);
      if (response.status === 200) {
        this.posts = data.posts;
        this.totalPages = data.totalPages;
        this.error = false;
        return;
      }
      this.error = true;
    },
    updatePage(number) {
      this.page = number;
    },
  },
};
</script>
