<script>
export default {
  name: "TableRowHistory",
  props: ["histories", "index"],
  computed: {
    formatedDate: function () {
      let formatedDate = new Date(this.histories.createdAt);
      let date = formatedDate.getDate();
      let month = formatedDate.getMonth();
      let year = formatedDate.getFullYear();
      let hour = formatedDate.getHours();
      let minutes = formatedDate.getMinutes();
      let second = formatedDate.getSeconds();
      return `${date}/${month}/${year} ${hour}:${minutes}:${second}`;
    },
  },
};
</script>
<template>
  <tr>
    <td class="p-3 text-xs">{{ index + 1 }}</td>
    <td class="p-3 text-xs">{{ histories.name }}</td>
    <td class="p-3 text-xs">{{ histories.description }}</td>
    <td class="p-3 text-xs">{{ histories.updatedBy }}</td>
    <td class="p-3 text-xs">{{ formatedDate }}</td>
  </tr>
</template>
