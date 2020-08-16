<template>
  <form
    class="form-signin text-center"
    @submit.prevent="register"
  >
    <div v-if="errorMessage" class="alert alert-danger">
      {{ errorMessage }}
    </div>
    <div v-else-if="successMessage" class="alert alert-success">
      {{ successMessage }}
    </div>

    <h1 class="h3 mb-3 font-weight-normal">Register</h1>

    <label
      for="inputEmail"
      class="sr-only"
    >Email address</label>
    <input
      type="email"
      id="inputEmail"
      class="form-control"
      placeholder="Email address"
      v-model="email"
      required
      autofocus
    >

    <label
      for="inputPassword"
      class="sr-only"
    >Password</label>
    <input
      type="password"
      id="inputPassword"
      class="form-control"
      placeholder="Password"
      v-model="password"
      required
    >
    <button
      class="btn btn-lg btn-primary btn-block"
      type="submit"
    >Register</button>
  </form>
</template>

<script>
export default {
  name: 'RegistrationPage',
  data() {
    return {
      email: '',
      password: '',
      errorMessage: '',
      successMessage: '',
    };
  },
  created() {
    document.getElementsByTagName('html')[0].classList.add('registration');
  },
  methods: {
    register() {
      if (!this.email.trim() || !this.password.trim()) {
        this.errorMessage = 'Email and password are required';
        return;
      }

      this.errorMessage = '';

      const user = {
        email: this.email,
        password: this.password,
      };

      localStorage.setItem('user', JSON.stringify(user));

      this.successMessage = 'Registration successful';

      this.email = '';
      this.password = '';
    },
  },
};
</script>

<style lang="scss">
html.registration {
  &,
  body {
    height: 100%;
  }

  body {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-align: center;
    align-items: center;
    padding-top: 40px;
    padding-bottom: 40px;
    background-color: #f5f5f5;
    justify-content: center;
  }
}
</style>

<style lang="scss" scoped>
.form-signin {
  max-width: 100%;
  width: 330px;
  padding: 15px;
  margin: auto;
}
.form-signin .checkbox {
  font-weight: 400;
}
.form-signin .form-control {
  position: relative;
  box-sizing: border-box;
  height: auto;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
