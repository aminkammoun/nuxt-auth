<template>
  <section class="container">
    <div>
      <b-form>
        <b-form-group
          description="Let us know your Email."
          label="Enter your Email"
          label-for="username"
        >
          <b-form-input
            id="username"
            v-model="email"
            type="email"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group
          description="Let us know your Password."
          label="Enter your Password"
          label-for="pw"
        >
          <b-form-input id="pw" v-model="password" type="password">
          </b-form-input>
        </b-form-group>
        <b-button-group size="sm">
          <b-button @click="login" variant="outline-success">Login</b-button>
          <b-button @click="check" variant="outline-success">Check</b-button>
        </b-button-group>
      </b-form>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      email: '',
      password: '',
    }
  },
  mounted() {},
  watch: {},
  components: {},
  methods: {
    async login() {
      try {
        this.$toast.show('Logging in...', { icon: 'fingerprint' })
        console.log(this.email, this.password)
        await this.$auth
          .loginWith('local', {
            data: {
              email: this.email,
              password: this.password,
            },
          })
          .catch((e) => {
            this.$toast.error('Failed Logging In', { icon: 'error_outline' })
          })
        if (this.$auth.loggedIn) {
          this.$toast.success('Successfully Logged In', { icon: 'done' })
        }
      } catch (e) {
        this.$toast.error('Username or Password wrong', { icon: 'error' })
      }
    },
    check() {
      console.log(this.$auth)
    },
    logout() {
      this.$toast.show('Logging out...', { icon: 'fingerprint' })
      this.$auth.logout()
    },
  },
}
</script>
<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
