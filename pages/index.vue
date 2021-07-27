<template>
  <div>
    <p>loggedIn - {{ $auth.loggedIn }}</p>
    <hr />
    <div>
      <h3>Login</h3>
      <input v-model="email" type="text" />
      <br />
      <input v-model="password" type="text" />
      <br />
      <button @click="onLogin">Login</button>
    </div>
    <div>
      <button @click="onFetchUser">Fetch User</button>
      <p>{{ user }}</p>
    </div>
    <div>
      <button @click="onFetchAuthTime">Fetch Auth Time</button>
      <p>{{ authTime }}</p>
    </div>
    <div>
      <button @click="onFetchNoAuthTime">Fetch No-Auth Time</button>
      <p>{{ noAuthTime }}</p>
    </div>
  </div>
</template>

<script>
export default {
  auth: false,
  data() {
    return {
      email: 'romaguera.haylie@example.com',
      password: 'password',
      user: null,
      authTime: null,
      noAuthTime: null,
    }
  },
  methods: {
    onLogin() {
      this.$auth.loginWith('laravelJWT', {
        data: {
          email: this.email,
          password: this.password,
        },
      })
    },
    async onFetchUser() {
      this.user = await this.$axios.$post('/laravel/api/auth/me')
    },
    async onFetchAuthTime() {
      this.authTime = await this.$axios.$get('/laravel/api/auth/time')
    },
    async onFetchNoAuthTime() {
      this.noAuthTime = await this.$axios.$get('/laravel/api/no-auth/time')
    },
  },
}
</script>
