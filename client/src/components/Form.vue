<script>
export default {
  name: "Form",
  emits: ["update-product", "create-product", "edit-product"],
  props: ["products", "categories"],
  computed: {
    getProduct() {
      return {
        name: this.products?.name,
        description: this.products?.description,
        imgUrl: this.products?.imgUrl,
        price: this.products?.price,
        categoryId: this.products?.categoryId,
      };
    },
  },
  methods: {
    postHandler: function () {
      if (this.products) {
        this.$emit("update-product", {
          name: this.getProduct?.name,
          description: this.getProduct?.description,
          imgUrl: this.getProduct?.imgUrl,
          price: this.getProduct?.price,
          categoryId: this.getProduct?.categoryId,
        });
      } else {
        this.$emit("create-product", {
          name: this.getProduct?.name,
          description: this.getProduct?.description,
          imgUrl: this.getProduct?.imgUrl,
          price: this.getProduct?.price,
          categoryId: this.getProduct?.categoryId,
        });
      }
    },
    updateProduct: async function () {
      this.$emit("edit-product");
    },
  },
};
</script>
<template>
  <div
    aria-hidden="true"
    class="justify-center flex items-center h-screen md:h-full md:inset-0"
  >
    <div class="relative px-4 w-full max-w-md h-full md:h-auto">
      <div class="relative bg-white rounded-lg shadow dark:bg-gray-1200">
        <form
          @submit.prevent="postHandler"
          class="px-6 pb-7 space-y-6 lg:px-8 sm:pb-6 xl:pb-8"
        >
          <h3 class="text-xl font-medium text-gray-900 text-center pt-10">
            Form Product
          </h3>
          <div class="flex justify-between">
            <div class="flex items-start">
              <input
                v-model="getProduct.name"
                id="name"
                type="text"
                name="name"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-purple-600 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mr-3"
                placeholder="Enter name"
              />
              <input
                v-model="getProduct.price"
                id="price"
                type="number"
                name="price"
                placeholder="Price"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-purple-600 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mr-3"
              />
            </div>
          </div>
          <div class="flex justify-between">
            <div class="flex items-start">
              <textarea
                v-model="getProduct.description"
                class="flex-1 appearance-none border border-gray-300 w-full py-2 px-4 bg-white text-gray-700 placeholder-gray-400 rounded-lg text-base focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent mb-2"
                id="description"
                placeholder="Enter Product description"
                name="description"
                rows="5"
                cols="40"
              >
              </textarea>
            </div>
          </div>
          <div class="flex justify-between">
            <div class="flex items-start">
              <input
                v-model="getProduct.imgUrl"
                id="imgUrl"
                type="text"
                name="imgUrl"
                placeholder="Image Url"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-purple-600 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mr-3"
              />
              <select
                v-model="getProduct.categoryId"
                id="categoryId"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 w-full"
              >
                <option
                  v-for="category in categories"
                  :key="category.id"
                  class="w-full"
                  :value="category.id"
                >
                  {{ category.name }}
                </option>
              </select>
            </div>
          </div>

          <div class="flex justify-center item-center">
            <button
              class="bg-blue-400 rounded-md text-gray-900 p-1 text-sm w-24 mr-2"
            >
              Submit
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
