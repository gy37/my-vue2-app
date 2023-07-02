<template>
  <div>
    <div v-if="loginType === 'username'">
      <label>Username</label>
      <input placeholder="Enter your username" key="username-input" />
    </div>
    <div v-else>
      <label>Email</label>
      <input placeholder="Enter your email address" key="email-input" />
    </div>
    <button v-on:click="toggleLoginType">Toggle login type</button>
  </div>
</template>

<script>
export default {
  name: 'VIF',
  data: function () {
    return {
      loginType: '',
    }
  },
  methods: {
    toggleLoginType: function () {
      this.loginType = this.loginType === 'username' ? 'email' : 'username';
    }
  }
}
</script>

<style lang="scss" scoped></style>