<template>
<div class="all">
  <head>
    <br />
    <br />
    <br />
  </head>
  <body>
    <br />
    <br />
    <h1 id="heading">Login</h1>
    <div class="container">
      <form>
        <div class="form-group col-md-12">
          <label for="Username">Username:</label>
          <input
            type="text"
            class="form-control"
            id="username-input"
            aria-describedby="userHelp"
            placeholder="Enter username"
            v-model="username"
          />
          <small id="userHelp" class="form-text text-muted">Type your username to login</small>
          <div
            class="error"
            v-if="$v && $v.username.$dirty && !$v.username.required"
          >Username is required</div>
        </div>
        <div class="form-group col-md-12">
          <label for="Password">Password</label>
          <input
            type="password"
            class="form-control"
            id="password-input"
            placeholder="Password"
            v-model="password"
          />
          <div
            class="error"
            v-if="$v && $v.password.$dirty && !$v.password.required"
          >Password is required</div>
        </div>
        <span id="submit-button">
          <button @click="isValid" class="btn btn-success m-2" type="button">Login</button>
        </span>
      </form>
    </div>
  </body>
</div>
</template>

<script>
import Vue from "vue";
import Vuelidate from "vuelidate";
import { required } from "vuelidate/lib/validators";
Vue.use(Vuelidate);

export default {
  data() {
    return {
      username: "",
      password: ""
    };
  },
  validations: {
    username: {
      required
    },
    password: {
      required
    }
  },
  methods: {
    isValid() {
      this.$v.$touch();
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border-radius: 5px;
}
.container {
  position: relative;
  width: 400px;
  background: white;
  padding: 60px40px;
  height: 400px;
  justify-content: center;
  align-items: center;
}
.all {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #ffdae0;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 800 400'%3E%3Cdefs%3E%3CradialGradient id='a' cx='396' cy='281' r='514' gradientUnits='userSpaceOnUse'%3E%3Cstop offset='0' stop-color='%23dd7ea4'/%3E%3Cstop offset='1' stop-color='%23ffdae0'/%3E%3C/radialGradient%3E%3ClinearGradient id='b' gradientUnits='userSpaceOnUse' x1='400' y1='148' x2='400' y2='333'%3E%3Cstop offset='0' stop-color='%23e1c4ff' stop-opacity='0'/%3E%3Cstop offset='1' stop-color='%23e1c4ff' stop-opacity='0.5'/%3E%3C/linearGradient%3E%3C/defs%3E%3Crect fill='url(%23a)' width='800' height='400'/%3E%3Cg fill-opacity='0.4'%3E%3Ccircle fill='url(%23b)' cx='267.5' cy='61' r='300'/%3E%3Ccircle fill='url(%23b)' cx='532.5' cy='61' r='300'/%3E%3Ccircle fill='url(%23b)' cx='400' cy='30' r='300'/%3E%3C/g%3E%3C/svg%3E");
  background-attachment: fixed;
  background-size: cover;
}
#heading {
  text-align: center;
  font-size: 60px;
}
</style>
