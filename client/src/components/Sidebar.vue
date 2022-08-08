<script>
export default {
  name: "Sidebar",
  emits: ["display-page"],
  methods: {
    displayPage: function (pageName) {
      this.$emit("display-page", pageName);
    },
  },
};
</script>
<template>
  <div class="lg:block my-4 ml-4 shadow-lg relative w-80 h-full">
    <div class="h-screen bg-white rounded-2xl dark:bg-gray-700">
      <div class="flex items-center justify-center pt-6"></div>
      <p class="flex items-center justify-center pt-6">DHafla Store</p>
      <nav class="mt-4">
        <div>
          <a
            @click.prevent="displayPage('main')"
            class="w-full font-thin text-blue-500 flex items-center p-4 my-2 transition-colors duration-50 justify-start bg-gradient-to-r from-white to-blue-50 border-r-4 border-blue-700 dark:from-gray-700 dark:to-gray-800 border-r-4 border-blue-250"
          >
            <span class="mx-4 text-sm font-normal"> Dashboard </span>
          </a>
          <a
            @click.prevent="displayPage('listProducts')"
            class="w-full font-thin text-blue-500 flex items-center p-4 my-2 transition-colors duration-200 justify-start bg-gradient-to-r from-white to-blue-100 border-r-4 border-blue-500 dark:from-gray-700 dark:to-gray-800 border-r-4 border-blue-500"
          >
            <span class="mx-4 text-sm font-normal"> List Product </span>
          </a>
          <a
            @click.prevent="displayPage('listCategory')"
            class="w-full font-thin text-blue-500 flex items-center p-4 my-2 transition-colors duration-200 justify-start bg-gradient-to-r from-white to-blue-100 border-r-4 border-blue-500 dark:from-gray-700 dark:to-gray-800 border-r-4 border-blue-500"
          >
            <span class="mx-4 text-sm font-normal"> List Categories </span>
          </a>
          <a
            @click.prevent="displayPage('listHistory')"
            class="w-full font-thin text-blue-500 flex items-center p-4 my-2 transition-colors duration-200 justify-start bg-gradient-to-r from-white to-blue-100 border-r-4 border-blue-500 dark:from-gray-700 dark:to-gray-800 border-r-4 border-blue-500"
          >
            <span class="mx-4 text-sm font-normal"> History </span>
          </a>
        </div>
      </nav>
    </div>
  </div>
</template>

<style></style>
