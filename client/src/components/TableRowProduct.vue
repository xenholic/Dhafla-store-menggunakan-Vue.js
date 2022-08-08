<script>
export default {
  name: "TableRowProduct",
  data() {
    return {
      status: ["active", "inactive", "archived"],
    };
  },
  emits: ["change", "edit-product", "display-page"],
  props: ["products"],
  methods: {
    displayPage: function (pageName) {
      this.$emit("display-page", pageName);
    },
    statusChange() {
      this.$emit("change", this.products.status, this.products.id);
    },
    editProductHandler: async function (id) {
      this.$emit("edit-product", id);
    },
  },
};
</script>
<template>
  <tr>
    <td class="p-2 text-xl text-left">
      <img :src="products.imgUrl" alt="ImageUrl" width="250" class="p-3" />{{
        products.name
      }}
    </td>
    <td class="p-3 text-xs">{{ products.description }}</td>
    <td class="p-3 text-xs">{{ products.price }}</td>
    <td class="p-3 text-xs">{{ products.Category.name }}</td>
    <td class="p-3 text-xs">{{ products.User.username }}</td>
    <td class="p-3">
      <select
        class="bg-gray-50 border border-gray-300 text-gray-900 text-xs rounded-lg focus:border-blue-500 text-xs"
        v-model="products.status"
        @change="statusChange"
      >
        <option v-for="(status, index) in status" :key="index" :value="status">
          {{ status }}
        </option>
      </select>
    </td>
    <td class="p-3">
      <button
        class="bg-green-200 p-2 rounded-md text-xs"
        @click.prevent="
          displayPage('editFormProduct');
          editProductHandler(products.id);
        "
      >
        Edit
        <i class="far fa-edit"></i>
      </button>
    </td>
  </tr>
</template>

<style></style>
