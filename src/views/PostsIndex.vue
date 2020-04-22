<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="post in filterBy(posts, $parent.titleFilter, 'title')" v-on:click="currentPost = post" v-bind:class="{selected: currentPost === post}">
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
  .selected {
    color: white;
    background-color: steelBlue;
    transition: background-color 1s ease;
  }
</style>
<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Welcome to Vue.js PostIndex!",
      posts: [],
      currentPost: {}
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