<template>
  <div class="container">
    <div class="row align-items-center min-vh-100">
      <div class="col-12 col-sm-8 col-md-6 col-lg-4 offset-0 offset-sm-2 offset-md-3 offset-lg-4">
        <form @submit.prevent="logInUser">
          <div class="mb-3 text-center">
            <img src="http://international.donstu.ru/wp-content/uploads/2019/01/IMG_4963.png" alt="DSTU Logo" class="logo">
            <h1>DSTU Todo list</h1>
          </div>
          <hr />
          <div class="mb-3">
            <label class="form-label" for="email">Email</label>
            <input
              class="form-control"
              type="email"
              name="email"
              id="email"
              v-model="email"
              placeholder="name@example.com"
              required
            />
          </div>
          <div class="mb-4">
            <label class="form-label" for="password">Password</label>
            <div class="input-group mb-3">
              <input
                :type="this.isPasswordVisible ? 'text' : 'password'"
                class="form-control"
                name="password"
                placeholder="Your password"
                v-model="password"
                required
              />
              <div class="input-group-text">
                <input
                  class="form-check-input mt-0 me-2"
                  type="checkbox"
                  aria-label="Checkbox for following text input"
                  v-model="this.isPasswordVisible"
                />Show
              </div>
            </div>
          </div>
          <div class="d-flex justify-content-center align-items-center">
            <button class="btn btn-primary">Sign In</button>
            <span class="ms-3 text-end">
              Not registered yet?
              <router-link to="/sign-up" class="btn btn-primary">Sign Up</router-link>
            </span>
          </div>
        </form>

      </div>
    </div>

  </div>

</template>

<script>

import axios from "axios";

export default {
  
  name: "SignInView",

  setup() {
    let isUserLogged = false;
  },

  data() {
    return {
      email: "",
      password: "",
      isPasswordVisible: false,
    };
  },

  methods: {

    async logInUser() {
      let isUserLogged = false;

      const data = await axios.get(
          'http://localhost:19452/api/Authentication/login',
            {email:this.email,
            password:this.password})
              .then(function (response) {
                localStorage.setItem("userToken", response.data.token)
            })
              .catch(function (error) {
                console.log(error);
            });
        
      await this.$$router.push('/');
    },
  }
  
}

  </script>

  <style scoped>
    .logo {
      width: 100px;
    }

  </style>