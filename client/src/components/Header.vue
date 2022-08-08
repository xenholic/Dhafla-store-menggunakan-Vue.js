<script>
import Btn from "./Button.vue";
export default {
  name: "Header",
  methods: {
    logoutHandler() {
      this.$emit("log-out");
    },
  },
  props: ["user"],
  components: { Btn },
};
</script>
<template>
  <div
    class="w-full shadow-lg bg-white dark:bg-gray-700 items-center h-16 rounded-2xl z-40"
  >
    <div
      class="relative z-20 flex flex-col justify-center h-full px-3 mx-auto flex-center"
    >
      <div
        class="relative items-center pl-1 flex w-full lg:max-w-68 sm:pr-2 sm:ml-0"
      >
        <div class="container relative flex w-3/4 h-auto h-full">
          <div class="relative flex items-center w-full lg:w-64 h-full group">
            <p>DHafla Store</p>
          </div>
        </div>

        <span
          class="bg-blue-100 text-blue-800 text-md font-semibold mr-2 px-2.5 py-0.5 rounded dark:bg-blue-200 dark:text-blue-800"
          >{{ user.username }}</span
        >
        <span
          class="bg-blue-100 text-blue-800 text-md font-semibold mr-2 px-2.5 py-0.5 rounded dark:bg-blue-200 dark:text-blue-800"
          >{{ user.email }}</span
        >
        <span
          class="bg-blue-100 text-blue-800 text-md font-semibold mr-2 px-2.5 py-0.5 rounded dark:bg-blue-200 dark:text-blue-800"
          >{{ user.role }}</span
        >

        <div class="z-10 w-24 text-base divide-y divide-gray-100">
          <button>
            <a @click="logoutHandler">Sign out</a>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
