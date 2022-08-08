<script>
import TableRowCategory from "./TableRowCategory.vue";
export default {
  name: "TableCategory",
  components: {
    TableRowCategory,
  },
  props: ["categories"],
};
</script>
<template>
  <div class="container mx-auto px-4 sm:px-8 max-w-full">
    <div class="py-8">
      <div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
        <div class="inline-block min-w-full shadow rounded-lg overflow-hidden">
          <table class="min-w-full leading-normal">
            <thead>
              <tr>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Category Number
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Category Name
                </th>
              </tr>
            </thead>
            <tbody>
              <TableRowCategory
                v-bind:categories="category"
                v-for="category in categories"
                :key="category.id"
              ></TableRowCategory>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
