<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <h1>{{ post }}</h1>
    <a  v-if="post.user_id === $parent.getUserId()" v-bind:href="`/posts/${post.id}/edit`">Edit this Post</a>
    <!--  -->
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js Show Page!!",
      post: {}
    };
  },
  created: function() {
    axios.get('/api/posts/' + this.$route.params.id).then(response => {
      console.log(response.data);
      this.post = response.data;
      console.log('post user id');
      console.log(this.post.user_id);
      console.log('current_user id');
      console.log(this.$parent.getUserId());
    });
  },
  methods: {}
};
</script>