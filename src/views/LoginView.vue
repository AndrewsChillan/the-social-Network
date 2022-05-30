<template>
  <h1>Connection</h1>
  <!-- Login form -->
  <form @submit.prevent="login">
    <div>
      <label for="email">Email</label>
      <input
        type="email"
        id="email"
        v-model="email"
        placeholder="abcd@nomdomaine.com"
      />
    </div>
    <div>
      <label for="password">Password</label>
      <input
        type="password"
        id="password"
        v-model="password"
        placeholder="1234"
      />
    </div>
    <button>Se connecter</button>
  </form>
  <p v-show="errorMessage != null">{{ errorMessage }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      errorMessage: null,
    };
  },
  methods: {
    async login() {
      const options = {
        method: "POST",
        headers: {
          "content-Type": "application/json",
        },
        body: JSON.stringify({
          email: this.email,
          password: this.password,
        }),
      };
      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/demo/login",
        options
      );

      const data = await response.json();

      if (response.status === 200) {
        localStorage.setItem("@social-network:token", data.token);
        this.$router.replace("/");
        return;
      }
      this.errorMessage = data.message;
    },
  },
};
</script>
