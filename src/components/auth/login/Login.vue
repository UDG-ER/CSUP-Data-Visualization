<template>
  <form @submit.prevent="onsubmit">
    <va-input
      v-model="username"
      type="text"
      :label="$t('auth.username')"
      :error="!!usernameErrors.length"
      :error-messages="usernameErrors"
    />

    <va-input
      v-model="password"
      type="password"
      :label="$t('auth.password')"
      :error="!!passwordErrors.length"
      :error-messages="passwordErrors"
    />

    <div class="auth-layout__options d-flex align--center justify--space-between">
      <!--
    <va-checkbox v-model="keepLoggedIn" class="mb-0" :label="$t('auth.keep_logged_in')"/>
    <router-link class="ml-1 link" :to="{name: 'recover-password'}">{{$t('auth.recover_password')}}</router-link>
      -->
    </div>

    <div class="d-flex justify--center mt-3">
      <va-button type="submit" class="my-0">{{ $t('auth.login') }}</va-button>
    </div>
  </form>
</template>

<script>
import config from '../../../config.json'

export default {
  name: "login",
  data() {
    return {
      api_url: config.api_url,
      username: "",
      password: "",
      keepLoggedIn: false,
      usernameErrors: [],
      passwordErrors: []
    };
  },
  computed: {
    formReady() {
      return !this.usernameErrors.length && !this.passwordErrors.length;
    }
  },
  methods: {
    authorize: async function(username, password) {
      const auth_api = this.api_url + "/api/account/login";

      try {
        const response = await fetch(auth_api, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json"
          },
          body: JSON.stringify({ Username: username, Password: password })
        });
        const result = await response.json();
        //this.token = result.Token;
        localStorage.setItem("jwt", result.Token);
        localStorage.setItem("username", username);
      } catch (error) {
        console.log("Error with getting token:" + error);
      }
    },

    async onsubmit() {
      this.usernameErrors = this.username ? [] : ["Username is required"];
      this.passwordErrors = this.password ? [] : ["Password is required"];
      if (!this.formReady) {
        return;
      }
      await this.authorize(this.username, this.password)
      this.$router.push({ name: "devices" });
    }
  }
};
</script>

<style lang="scss">
</style>
