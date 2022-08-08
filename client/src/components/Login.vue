<script>
import Btn from "./Button.vue";
export default {
  name: "login",
  data() {
    return {
      user: {
        email: "",
        password: "",
      },
    };
  },
  emits: ["display-page", "login-user"],
  components: { Btn },
  methods: {
    displayPage: function (pageName) {
      this.$emit("display-page", pageName);
    },
    loginChild() {
      this.$emit("login-user", {
        email: this.user.email,
        password: this.user.password,
      });
    },
  },
};
</script>

<template>
  <div class="flex h-screen w-screen justify-center items-center p-6">
    <div
      class="w-full lg:max-w-md px-4 py-8 border-t bg-white border-purple-600 shadow-lg shadow-purple-800/50 rounded-lg shadow dark:bg-gray-800 md:px-8 items-center justify-center"
    >
      <div class="text-3xl font-semibold text-center text-purple-700">
        LOGIN FORM
      </div>
      <div class="mt-8">
        <form @submit.prevent="loginChild">
          <div class="flex flex-col mb-2">
            <div class="flex relative">
              <input
                v-model="user.email"
                type="email"
                id="username"
                name="username"
                class="rounded-r-lg w-full shadow-sm"
                placeholder="Your username"
              />
            </div>
          </div>
          <div class="flex flex-col mb-6">
            <div class="flex relative">
              <input
                v-model="user.password"
                name="password"
                type="password"
                id="password"
                class="rounded-r-lg w-full shadow-sm"
                placeholder="Your password"
              />
            </div>
          </div>
          <div class="flex w-full">
            <Btn
              type="submit"
              class="py-2 px-2 bg-purple-600 text-white w-full text-center rounded-lg"
              >Login</Btn
            >
          </div>
          <div class="flex w-full mt-4 mx-auto items-center justify-center">
            <div id="google-button"></div>
          </div>
        </form>
      </div>
      <div class="flex items-center justify-center mt-6">
        <button
          @click="displayPage('registration')"
          class="inline-flex cursor:pointer items-center text-xs font-thin text-center text-gray-500 hover:text-gray-700 dark:text-gray-100 dark:hover:text-white"
        >
          <span class="ml-2"> You don&#x27;t have an account? </span>
        </button>
      </div>
    </div>
  </div>
</template>
