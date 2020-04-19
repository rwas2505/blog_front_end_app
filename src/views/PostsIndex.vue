<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="post in posts">
      <p>id: {{ post.id }}</p>
      <p>title: <a v-bind:href="`/posts/${post.id}`">{{ post.title }}</a></p>
      <p>body: {{ post.body }}</p>
      <img v-bind:src="post.image">
      <hr>
      <hr>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js PostIndex!",
      posts: []
    };
  },
  created: function() {
    console.log("This is in the created function");
    axios.get('/api/posts').then(response => {
      console.log(response.data);
      this.posts = response.data;
    });
  },
  methods: {}
};
</script>