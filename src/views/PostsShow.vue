<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <h1>{{ post }}</h1>
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
    });
  },
  methods: {}
};
</script>