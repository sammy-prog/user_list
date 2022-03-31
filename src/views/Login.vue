<template>
  <div class="login">
    <div class="login__container">
      <h2>SIGN IN TO CREATE YOUR ACCOUNT</h2>
      <p style="color: red;margin-top:20px" v-if="error != ''">{{error}}</p>
      <input
        v-model="username"
        type="text"
        placeholder="johhnythedesigner@gmail.com"
      />
      <br />
      <input
        v-model="password"
        type="password"
        placeholder="**************"
      />
      <br />
      <div class="login__container__checkbox">
        <input type="checkbox" checked />
        <p class="login__container__checkbox--text">Keep me signed in</p>
      </div>
      <button @click="loginUser">SIGN IN</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      username: "",
      password: "",
      error: ''
    };
  },
  methods: {
    loginUser() {
      this.error = '';
      if(this.username =="admin" && this.password=="1234") {
        localStorage.setItem('isUserAuthenticated', true);
        this.error = ''
        this.$router.push('/');
      } else {
        this.error = 'Login failed please try again';
      }
    },
    clearError() {
      this.error = ''
    }
  },
  watch: {
    error() {
      const myTimeout = setTimeout(this.clearError, 2500);
    }
  }
};
</script>
<style>
* {
  overflow-x: hidden;
}
.login {
  margin-top: 20vh;
  text-align: center;
}
.login__container {
  width: 50%;
  margin: auto;
}
.login__container input {
  margin-top: 20px;
  padding: 20px;
  width: 400px;
  border-radius: 5px;
  background-color: rgb(230, 230, 230);
  border: 0px;
}
.login__container button {
  margin-top: 70px;
  width: 30vw;
  padding: 20px;
  background-color: #746bde;
  border: 0px;
  border-radius: 5px;
  color: white;
  cursor: pointer;
}
.login__container__checkbox {
  display: inline-block;
}

@media only screen and (max-width: 600px) {
  .login__container {
    width: 90%;
    margin: auto;
  }
  .login__container__checkbox {
    margin-left: -120px;
  }
}
</style>