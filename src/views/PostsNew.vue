<template>
  <div class="new-blog">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Blog Post</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>title:</label> 
          <input type="text" class="form-control" v-model="title">
        </div>
        <div class="form-group">
          <label>body:</label>
          <input type="text" class="form-control" v-model="body">
        </div>
        <div class="form-group">
          <label>image url:</label>
          <input type="text" class="form-control" v-model="imageUrl">
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
      title: "",
      body: "",
      imageUrl: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.imageUrl
      };
      axios
        .post("/api/posts", params)
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