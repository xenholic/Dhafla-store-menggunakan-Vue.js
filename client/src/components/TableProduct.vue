<script>
import TableRowProduct from "./TableRowProduct.vue";
import Btn from "./Button.vue";
import Form from "./Form.vue";
export default {
  name: "TableProduct",
  components: {
    TableRowProduct,
    Form,
    Btn,
  },
  emits: ["change", "edit-product", "display-page"],
  props: ["products"],
  data() {
    return {
      page: "login",
    };
  },
  methods: {
    displayPage: function (pageName) {
      this.$emit("display-page", pageName);
    },
    statusChange(newStatus, idProduct) {
      this.$emit("change", newStatus, idProduct);
    },
    editProductHandler: async function (id) {
      this.$emit("edit-product", id);
    },
  },
};
</script>
<template>
  <!-- Start table Product -->
  <div class="container mx-auto px-4 sm:px-8 max-w-full">
    <div class="py-8">
      <div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
        <div class="flex w-sm">
          <Btn
            @click="displayPage('formAddProduct')"
            type="button"
            class="py-2 px-3 bg-purple-600 text-white w-1/10 text-center mb-4 rounded-lg"
          >
            Add Product
          </Btn>
        </div>
        <div class="inline-block min-w-full shadow rounded-lg overflow-hidden">
          <table class="min-w-full leading-normal">
            <thead>
              <tr>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Name
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Description
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Price
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Category
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Author
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Status
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Action
                </th>
              </tr>
            </thead>
            <tbody v-for="product in products" :key="product.id">
              <TableRowProduct
                v-bind:products="product"
                @display-page="displayPage"
                @change="statusChange"
                @edit-product="editProductHandler"
              ></TableRowProduct>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
