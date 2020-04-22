<template>
  <div id="app">
    <div id="nav">
      <!-- <router-link to="/">Home</router-link> | -->
      <!-- <router-link to="/about">About</router-link> | -->
      <router-link to="/signup">Signup</router-link> | 
      <router-link to="/login">Login</router-link> | 
      <router-link to="/logout">Logout</router-link> |
      <!-- <router-link to="/posts/new">Create New Post</router-link> -->
    </div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <a class="navbar-brand" href="/">Blog App</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="/posts">Posts Index <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/posts/new">New</a>
          </li>
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              Auth
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a v-if="!isLoggedIn()" class="dropdown-item" href="/login">Login</a>
              <a v-if="isLoggedIn()"class="dropdown-item" href="/logout">Logout</a>
              <div class="dropdown-divider"></div>
              <a v-if="!isLoggedIn()"class="dropdown-item" href="/signup">SignUp</a>
            </div>
          </li>
          <!-- <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li> -->
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>
    <p v-if="isLoggedIn()">I am logged in</p>
    <p v-if="!isLoggedIn()">I am not logged in</p>
    <router-view/>
  </div>
</template>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
  }
  body {
    background-image: url('./assets/tweed.png')
  }
</style>

<script>
export default {
  methods: {
    isLoggedIn: function() {
      console.log("I am checking if I'm logged in")
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function() {
      return parseInt(localStorage.getItem("user_id"));
    }
  }
};
</script>
