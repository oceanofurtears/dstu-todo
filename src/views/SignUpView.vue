<template>
  <div class="container">
    <div class="row align-items-center min-vh-100">
      <div
        class="col-12 col-sm-8 col-md-6 col-lg-4 offset-0 offset-sm-2 offset-md-3 offset-lg-4"
      >
        <form @submit.prevent="signUpUser">
          <div class="mb-3 text-center">
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
              placeholder="name@example.com"
              v-model="email"
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
                placeholder="Your secure password"
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
            <button type="submit" class="btn btn-primary">Sign Up</button>
            <button
              class="ms-3 btn btn-outline-danger"
              @click="this.$router.push('/sign-in')"
            >Cancel
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
    import {reactive} from 'vue';
    import {useRouter} from "vue-router";
    import axios from "axios";

export default {
  name: "SignUpView",

  data() {
    return {
      email: "",
      password: "",
      isPasswordVisible: false,
    };
  },
  
  methods: {

    async signUpUser() {

      let userList = [];
      let isUserFound = false;

      const data = await axios.post(
          'http://localhost:19452/api/Authentication/register',
           
          {email:this.email,
          password:this.password})
            .then(function (response) {
              alert("Пользователь успешно создан");
            })
            .catch(function (error) {
              console.log(error);
            });
          
        await this.$router.push('/sign-in')
      },
    }
  }

</script>