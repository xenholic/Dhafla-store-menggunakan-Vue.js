<script>
import TableRowHistory from "./TableRowHistory.vue";
export default {
  name: "TableHistory",
  components: {
    TableRowHistory,
  },
  props: ["histories"],
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
                  No
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Product Name
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
                  Updated By
                </th>
                <th
                  scope="col"
                  class="px-5 py-3 bg-white border-b border-gray-200 text-gray-800 text-left text-xs font-normal"
                >
                  Created At
                </th>
              </tr>
            </thead>
            <tbody>
              <TableRowHistory
                v-bind:histories="history"
                v-for="(history, index) in histories"
                :key="history.id"
                :index="index"
              ></TableRowHistory>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
  <!-- End table history-->
</template>

<style></style>
