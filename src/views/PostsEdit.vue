<template>
  <div class="new-blog">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>Edit Blog Post</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>title:</label> 
          <input type="text" class="form-control" v-model="post.title">
        </div>
        <div class="form-group">
          <label>body:</label>
          <input type="text" class="form-control" v-model="post.body">
        </div>
        <div class="form-group">
          <label>image url:</label>
          <input type="text" class="form-control" v-model="post.image">
        </div>
        <input type="submit" class="btn btn-primary" value="Submit">
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {},
      errors: []
    };
  },

  created: function() {
    console.log('in created on edit page')
    axios.get(`/api/posts/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.post = response.data;
    });
  },

  methods: {
    submit: function() {
      var params = {
        title: this.post.title,
        body: this.post.body,
        image: this.post.image
      };
      console.log('params');
      console.log(params);
      axios
        .patch(`/api/posts/${this.post.id}`, params)
        .then(response => {
          this.$router.push("/posts");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>