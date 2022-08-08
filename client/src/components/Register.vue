<script>
import Btn from "./Button.vue";
export default {
  name: "Register",
  components: {
    Btn,
  },
  data() {
    return {
      user: {
        username: "",
        email: "",
        phoneNumber: "",
        address: "",
        password: "",
      },
    };
  },
  emits: ["display-page", "registration-user"],
  methods: {
    displayPage: function (pageName) {
      this.$emit("display-page", pageName);
    },
    registration: function () {
      this.$emit("registration-user", {
        username: this.user.username,
        email: this.user.email,
        phoneNumber: this.user.phoneNumber,
        address: this.user.address,
        password: this.user.password,
      });
    },
  },
};
</script>

<template>
  <div class="flex justify-center h-screen w-screen items-center p-6">
    <div class="flex justify-center items-center p-6">
      <div
        class="w-full lg:max-w-md px-4 py-8 border-t bg-white border-purple-600 shadow-lg shadow-purple-800/50 rounded-lg shadow dark:bg-gray-800 md:px-8 items-center justify-center"
      >
        <div class="text-3xl font-semibold text-center text-purple-700">
          Register To Your Account
        </div>
        <div class="mt-8">
          <form @submit.prevent="registration">
            <div class="flex flex-row">
              <div class="flex flex-col mb-2 mr-2">
                <div class="flex relative">
                  <input
                    v-model="user.email"
                    name="email"
                    type="text"
                    id="email"
                    class="rounded-r-lg w-full shadow-sm"
                    placeholder="Your email"
                  />
                </div>
              </div>
              <div class="flex flex-col mb-2 mr-2">
                <div class="flex relative">
                  <input
                    v-model="user.username"
                    name="username"
                    type="text"
                    id="username-user"
                    class="rounded-r-lg w-full shadow-sm"
                    placeholder="Your username"
                  />
                </div>
              </div>
            </div>
            <div class="flex flex-row w-full">
              <div class="col-span-2 w-full">
                <label class="text-gray-700" for="address">
                  <textarea
                    v-model="user.address"
                    name="address"
                    class="rounded-r-lg w-full shadow-sm"
                    id="address"
                    placeholder="Enter your address"
                    rows="2"
                    cols="10"
                  >
                  </textarea>
                </label>
              </div>
            </div>
            <div class="flex flex-row">
              <div class="flex flex-col mb-6 mr-2">
                <div class="flex relative">
                  <input
                    v-model="user.phoneNumber"
                    name="phoneNumber"
                    type="text"
                    id="phoneNumber"
                    class="rounded-r-lg w-full shadow-sm"
                    placeholder="Your phone number"
                  />
                </div>
              </div>
              <div class="flex flex-col mb-6 mr-2">
                <div class="flex relative">
                  <input
                    v-model="user.password"
                    name="password"
                    type="password"
                    id="sign-in-email"
                    class="rounded-r-lg w-full shadow-sm"
                    placeholder="Your password"
                  />
                </div>
              </div>
            </div>
            <div class="flex w-md">
              <Btn
                type="button"
                class="py-2 px-2 bg-purple-600 text-white w-full text-center rounded-lg"
              >
                Submit
              </Btn>
            </div>
          </form>
        </div>
        <div class="flex items-center justify-center mt-6">
          <button
            @click="displayPage('login')"
            class="rounded-r-lg w-full shadow-sm"
          >
            <span class="ml-2"> You have an account? </span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
