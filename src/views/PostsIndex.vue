<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="post in posts">
      <!-- <p>id: {{ post.id }}</p>
      <p>title: <a v-bind:href="`/posts/${post.id}`">{{ post.title }}</a></p>
      <p>body: {{ post.body }}</p>
      <img v-bind:src="post.image"> -->
      <div class="card" style="width: 28rem;">
        <img v-bind:src="post.image">
        <div class="card-body">
          <h5 class="card-title">Title: <a v-bind:href="`/posts/${post.id}`">{{ post.title }}</a></h5>
          <p class="card-text">Body: {{ post.body }}</p>
          <!-- <a href="#" class="btn btn-primary">Go somewhere</a> -->
        </div>
      </div>
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