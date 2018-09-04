<template>
  <div class="card login">
    <header class="card-header">
      <p class="card-header-title">Authorization Required</p>
    </header>
    <div class="card-content">
      <div class="content">
        <form ref="form">
          <b-field label="Username" horizontal>
            <b-input v-model="username"></b-input>
          </b-field>
          <b-field label="Password" horizontal>
            <b-input type="password" v-model="password" password-reveal></b-input>
          </b-field>
          <b-field horizontal>
            <p class="control">
              <a class="button is-primary is-fullwidth" @click="submit">Login</a>
            </p>
            <p class="control">
              <a class="button is-primary is-fullwidth" @click="reset">Reset</a>
            </p>
          </b-field>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      username: '',
      password: ''
    }),
    methods: {
      submit() {
        this.$session.login(this.username, this.password).then(() => {
          this.$router.push('/');
        }).catch(() => {
          this.$toast.open({
            message: 'Invalid username and/or password! Please try again.',
            type: 'is-warning'
          });
        });
      },
      reset() {
        this.$refs.form.reset();
      }
    }
  };
</script>

<style>
  .login {
    width: 400px;
    left: 50%;
    margin-left: -200px;
    margin-top: 200px;
  }
</style>